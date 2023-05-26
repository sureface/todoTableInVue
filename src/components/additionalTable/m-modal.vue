<template>
  <div class="action__modals m__modal" @click="$emit('closeM2', $event)">
    <div class="action__modals-card" @click.stop>
      <div class="card__wrapper">
        <div class="card__wrapper_close m__close" @click="$emit('closeM2', $event)">
          <div>X</div>
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

          <b-form-group
              label="Size"
              label-for="size"
              invalid-feedback="Size is required"
              :state="nameState"
              class="mt-2 mb-2"
          >
            <b-form-select
                v-model="selected"
                :options="options"
                class="px-2 py-2 border border-secondary rounded-3 w-100"
                id="size"
            >
            </b-form-select>
          </b-form-group>

          <hr class="my-4">

          <div class="d-flex align-items-center justify-content-between">
            <div>
              <b-form-group label-for="datepicker" label="Deliver Date">
                <b-form-datepicker id="datepicker" v-model="selectDate" class="mb-2"></b-form-datepicker>
              </b-form-group>
            </div>
            <div>
              <b-form-group label-for="demo-sb" label="Choose Quantity">
                <b-form-spinbutton id="demo-sb" v-model="quantity" min="1" max="100"></b-form-spinbutton>
              </b-form-group>
            </div>
            <div>
              <b-form-group label="Color" label-for="chooseColor" class="mb-2">
                <b-form-radio-group
                    v-model="byDefaultColor"
                    :options="ChooseColor"
                    class="d-flex align-items-center gap-3"
                    value-field="item"
                    text-field="name"
                    id="chooseColor"
                ></b-form-radio-group>
              </b-form-group>
            </div>
          </div>

        </form>
        <div class="d-flex align-items-center justify-content-end mb-4">
          <button type="button" class="btn btn-success"  @click="submitProduct">Add</button>
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
      selected: null,
      options: [
        { value: null, text: 'Please select the Size', disabled: true },
        { value: 'a', text: '900x656' },
        { value: 'b', text: '1024x856' },
        { value: 'c', text: '1110x900' },
        { value: 'd', text: '1200x986' },
      ],
      selectDate: '',
      byDefaultColor: 'A',
      ChooseColor: [
        { item: 'A', name: 'Black' },
        { item: 'B', name: 'White' },
        { item: 'D', name: 'Blue' },
      ],
      quantity: 1,
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
      this.type = '';
      this.material = '';
      this.quantity = 1;
      this.byDefaultColor = '';
      this.selectDate = '';
      this.selected = '';
      this.nameState = null;
    },
    submitProduct() {
      if (!this.checkFormValidity()) {
        return
      }
      this.$emit('added-products',
          {
            name: this.name,
            type: this.type,
            material: this.material,
            size: this.currentValSize(),
            date: this.selectDate,
            color: this.currentValColor(),
            quantity: this.quantity,
            id: this.id,
          }
      )
      this.resetModal()
      this.$emit('closeM2', event)
    },
    editSelectedProducts() {
      if (Object.keys(this.selectedProducts).length) {
        this.name = this.selectedProducts.name;
        this.type = this.selectedProducts.type;
        this.material = this.selectedProducts.material;
        this.selected = this.currentValSize();
        this.selectDate = this.selectedProducts.date;
        this.byDefaultColor = this.currentValColor();
        this.quantity = this.selectedProducts.quantity;
        this.id = this.selectedProducts.id
      }
    },
    currentValSize() {
      const val = this.options.find(option => option.value === this.selected);
      return val.text
    },
    currentValColor() {
      const val = this.ChooseColor.find(option => option.item === this.byDefaultColor);
      return val.name
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