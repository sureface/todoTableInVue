<template>
  <div class="action__modals m__modal" @click="$emit('closeM2', $event)">
    <div class="action__modals-card" @click.stop>
      <div class="card__wrapper">
        <div class="card__wrapper_close m__close" @click="$emit('closeM2', $event)">
          <div>X</div>
        </div>
        <form ref="form"  class="mb-3">

          <b-form-group
              label="Type"
              label-for="type-input"
              invalid-feedback="type is required"
              :state="nameState"
              class="mb-2"
          >
            <b-form-input
                id="type-input"
                v-model="type"
                :state="nameState"
                required
                class="shadow-none"
            ></b-form-input>
          </b-form-group>
          <b-form-group
              label="Material"
              label-for="material-input"
              invalid-feedback="Material is required"
              :state="nameState"
              class="mb-2"
          >
            <b-form-input
                id="material-input"
                v-model="material"
                :state="nameState"
                required
                class="shadow-none"
            ></b-form-input>
          </b-form-group>
        </form>
        <div class="d-flex align-items-center justify-content-end mb-4">
          <button type="button" class="btn btn-success"  @click="submitProduct">Add Now</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "m-modal",
  props: {
    selectedProducts: Object,
  },
  data() {
    return {
      nameState: null,
      name: '',
      type: '',
      material: '',
      id: null,
    }
  },
  methods: {
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity()
      this.nameState = valid
      return valid
    },
    resetModal() {
      this.name = ''
      this.type = ''
      this.material = ''
      this.nameState = null
    },
    submitProduct() {
      if (!this.checkFormValidity()) {
        return
      }
      this.$emit('added-products', {name: this.name, type: this.type, material: this.material, id: this.id})
      this.resetModal()
      this.$emit('closeM2', event)
    },
    editSelectedProducts() {
      console.log(this.selectedProducts)
      if (Object.keys(this.selectedProducts).length) {
        this.name = this.selectedProducts.name;
        this.type = this.selectedProducts.type;
        this.material = this.selectedProducts.material;
        this.id = this.selectedProducts.id
      }
    },
  },
  mounted() {
    if (this.selectedProducts) {
      this.editSelectedProducts();
    }
  }
}
</script>

<style scoped>

</style>