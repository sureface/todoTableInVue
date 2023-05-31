<template>
  <div>
    <m-modal
      v-if="isOpen"
      :editedIndex="editedIndex"
      :editedEmployers="editedEmployers"
      @closeM2="closeModal2"
      @formData="margeAddress"
    />

    <div class="action__modals" @click="closeModal1">
      <div class="action__modals-card" @click.stop>
        <div class="card__wrapper">
          <div class="card__wrapper_close" @click.stop="closeModal1">
            <div>X</div>
          </div>
          <div class="text-center text-secondary text-lg">
            Do Something !
          </div>
          <form ref="form"  class="mb-3">
            <b-form-group
                label="Name"
                label-for="name-input"
                invalid-feedback="Name is required"
                class="mb-2"
            >
              <b-form-input
                  id="name-input"
                  v-model="editedEmployersData.name"
                  required
                  class="shadow-none"
              ></b-form-input>
            </b-form-group>
            <b-form-group
                label="Last Name"
                label-for="Lname-input"
                invalid-feedback="Last Name is required"
                class="mb-2"
            >
              <b-form-input
                  id="Lname-input"
                  v-model="editedEmployersData.last_name"
                  required
                  class="shadow-none"
              ></b-form-input>
            </b-form-group>
            <b-form-group
                label="Age"
                label-for="age-input"
                invalid-feedback="Age is required"
                class="mb-2"
            >
              <b-form-input
                  id="age-input"
                  v-model="editedEmployersData.age"
                  required
                  class="shadow-none"
              ></b-form-input>
            </b-form-group>
            <b-form-group
                label="Last Work Place"
                label-for="last-work-input"
                invalid-feedback="Last Work Place is required"
            >
              <b-form-input
                  id="last-work-input"
                  v-model="editedEmployersData.last_work_place"
                  required
                  class="shadow-none"
              ></b-form-input>
            </b-form-group>
          </form>

          <div class="mt-5 mb-5">
            <hr>
          </div>

          <div>

            <div class="text-center text-secondary text-lg">
              Add New Product ! &nbsp; &nbsp; ( optional )
            </div>

            <button class="btn btn-success mb-3" @click="isOpen = !isOpen">Add Product</button>

            <m-table
              :address="editedEmployersData.address"
              :editedIndex="editedIndex"
              @newAddress="margeAddress"
              @deletedAddress="updateAddress"
            />

          </div>

          <div class="d-flex align-items-center justify-content-end mt-4">
            <button type="button" class="btn btn-success" @click="submitForm">{{formTitle}}</button>
          </div>

        </div>
      </div>

    </div>
  </div>
</template>

<script>
import mTable from './additionalTable/m-table';
import mModal from './additionalTable/m-modal';

export default {
  name: "actionModals",
  props: {
    editedIndex: Number,
    editedEmployers: Object
  },
  components: {
    mTable,mModal
  },
  data() {
    return {
      editedEmployersData: {...this.editedEmployers},
      isOpen: false,
    }
  },
  computed: {
    formTitle() {
      return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
    }
  },
  methods: {
    closeModal1() {
      this.$emit('close_modal', event);
    },
    closeModal2(){
      this.isOpen = !this.isOpen
    },
    margeAddress(newAddress) {
      this.editedEmployersData.address.push(newAddress)
    },
    updateAddress(updateAddress) {
      this.editedEmployersData.address.push(updateAddress)
    },
    submitForm() {
      this.$emit('formData', this.editedEmployersData)
      this.$emit('close_modal', event)
    },
  },
}
</script>

<style scoped>

</style>