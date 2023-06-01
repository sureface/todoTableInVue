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
                v-model="editedM2.country"
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
                v-model="editedM2.street"
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
                v-model="editedM2.village"
                required
                class="shadow-none"
            ></b-form-input>
          </b-form-group>
        </form>
        <div class="d-flex align-items-center justify-content-end mb-4">
          <button type="button" class="btn btn-success" @click="m2FormSubmit"> {{title}} </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "m-modal",
  props: {
    editedIndexTable: Number,
    emptyM2: Object,
  },
  data() {
    return {
      m2index: -1,
      editedM2: {...this.emptyM2}
    }
  },
  computed: {
    title() {
      return this.editedIndexTable > this.m2index ? 'edit' : 'add'
    }
  },
  mounted() {
  },
  methods: {
    m2FormSubmit() {
      this.$emit('m2form', this.editedM2)
      this.$emit('closeM2', event)
    },
  },
}
</script>

<style scoped>

</style>