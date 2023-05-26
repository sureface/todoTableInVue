<template>
  <div>
    <m-modal
        @closeM2="closeM2"
        v-if="isOpenM2"
        @added-products="products"
    />

    <div class="action__modals" @click="$emit('close_modal', $event)">
      <div class="action__modals-card" @click.stop>
        <div class="card__wrapper">
          <div class="card__wrapper_close" @click.stop="$emit('close_modal', $event)">
            <div>X</div>
          </div>
          <div class="text-center text-secondary text-lg">
            Please Add New Employers
          </div>
          <form ref="form"  class="mb-3">
            <b-form-group
                label="Name"
                label-for="name-input"
                invalid-feedback="Name is required"
                :state="nameState"
                class="mb-2"
            >
              <b-form-input
                  id="name-input"
                  v-model="name"
                  :state="nameState"
                  required
                  class="shadow-none"
              ></b-form-input>
            </b-form-group>
            <b-form-group
                label="Last Name"
                label-for="Lname-input"
                invalid-feedback="Last Name is required"
                :state="nameState"
                class="mb-2"
            >
              <b-form-input
                  id="Lname-input"
                  v-model="last_name"
                  :state="nameState"
                  required
                  class="shadow-none"
              ></b-form-input>
            </b-form-group>
            <b-form-group
                label="Age"
                label-for="age-input"
                invalid-feedback="Age is required"
                :state="nameState"
                class="mb-2"
            >
              <b-form-input
                  id="age-input"
                  v-model="age"
                  :state="nameState"
                  required
                  class="shadow-none"
              ></b-form-input>
            </b-form-group>
            <b-form-group
                label="Last Work Place"
                label-for="last-work-input"
                invalid-feedback="Last Work Place is required"
                :state="nameState"
            >
              <b-form-input
                  id="last-work-input"
                  v-model="last_work_place"
                  :state="nameState"
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

            <button class="btn btn-success mb-3" @click="isOpenM2 = true">Add Product</button>

            <m-table
              :m2Products="m2_products"
            />

          </div>

          <div class="d-flex align-items-center justify-content-end mt-4">
            <button type="button" class="btn btn-success" @click="addNew">Add Now</button>
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
    selectedEmployee: Object,
  },
  components: {
    mTable,mModal
  },
  data() {
    return {
      id: null,
      name: '',
      last_name: '',
      age: null,
      last_work_place: '',
      nameState: null,
      isOpenM2: false,
      m2_products: []
    }
  },
  methods: {
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity()
      this.nameState = valid
      return valid
    },
    resetModal() {
      this.name = '';
      this.last_name = '';
      this.age = null;
      this.last_work_place = '';
      this.nameState = null;
    },
    addNew() {
      if (!this.checkFormValidity()) {
        return
      }
      this.$emit('added-employee', {name: this.name, last_name: this.last_name, age: this.age, last_work_place: this.last_work_place, id: this.id})
      this.resetModal();
      this.$emit('close_modal', event)
    },
    editSelectedEmployee() {
      if (Object.keys(this.selectedEmployee).length) {
        this.name = this.selectedEmployee.first_name;
        this.last_name = this.selectedEmployee.last_name;
        this.age = this.selectedEmployee.age;
        this.last_work_place = this.selectedEmployee.last_work_place;
        this.id = this.selectedEmployee.id
      }
    },
    closeM2() {
      this.isOpenM2 = false
    },
    products(form) {
      console.log(form, '1modal')

      form.id = this.m2_products.length + 1;

      this.m2_products.push(form)



    }
  },
  mounted() {
    this.editSelectedEmployee()
  }
}
</script>

<style scoped>

</style>