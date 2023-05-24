<template>
  <div class="action__modals" @click="$emit('close_modal', $event)">
    <div class="action__modals-card" @click.stop>
      <div class="card__wrapper">
        <div class="card__wrapper_close" @click.stop="$emit('close_modal', $event)">
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
        <div class="d-flex align-items-center justify-content-end">
          <button type="button" class="btn btn-success" @click="addNew">Add Now</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "actionModals",
  props: {
    selectedEmployee: Object,
  },
  data() {
    return {
      id: null,
      name: '',
      last_name: '',
      age: null,
      last_work_place: '',
      nameState: null,
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
      this.last_name = ''
      this.age = ''
      this.last_work_place = ''
      this.nameState = null
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
    }
  },
  mounted() {
    this.editSelectedEmployee()
  }
}
</script>

<style scoped>

</style>