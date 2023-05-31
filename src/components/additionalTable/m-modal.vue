<template>
  <div class="action__modals m__modal" @click="$emit('closeM2', $event)">
    <div class="action__modals-card" @click.stop>
      <div class="card__wrapper">
        <div class="card__wrapper_close m__close" @click="$emit('closeM2', $event)">
          <div>X</div>
        </div>
        <form ref="form"  class="mb-3">
          <b-form-group
              label="Country"
              label-for="name-input"
              invalid-feedback="Name is required"
              class="mb-2"
          >
            <b-form-input
                id="name-input"
                v-model="editedAddressData.country"
                required
                class="shadow-none"
            ></b-form-input>
          </b-form-group>
          <b-form-group
              label="Street"
              label-for="type-input"
              invalid-feedback="type is required"
              class="mb-2"
          >
            <b-form-input
                id="type-input"
                v-model="editedAddressData.street"
                required
                class="shadow-none"
            ></b-form-input>
          </b-form-group>
          <b-form-group
              label="Village"
              label-for="material-input"
              invalid-feedback="Material is required"
              class="mb-2"
          >
            <b-form-input
                id="material-input"
                v-model="editedAddressData.village"
                required
                class="shadow-none"
            ></b-form-input>
          </b-form-group>
        </form>
        <div class="d-flex align-items-center justify-content-end mb-4">
          <button type="button" class="btn btn-success"  @click="submitForm">{{ formTitle }}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "m-modal",
  props: {
    editedIndex: Number,
    editedAddress: Object,
  },
  data() {
    return {
      isOpen: false,
      editedAddressData: {...this.editedAddress}
    }
  },
  computed: {
    formTitle() {
      return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
    },
  },
  methods: {

    submitForm() {
      this.$emit('formData', this.editedAddressData)
      this.$emit('closeM2', event)
    }
  },
}
</script>

<style scoped>

</style>