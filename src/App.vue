<template>
  <div class="wrapper">

    <bg-video />

    <Modal
        :selectedEmployee="selectedEmployee"
        v-if="isOpen || isEdit"
        @close_modal="closeModal"
        @added-employee="handleAdd"

    />

    <div class="container">

      <div class="text-center mt-5 mb-5 text-secondary h2 text-uppercase">
        list of Employers to Google
      </div>

      <div class="apper">

        <header class="mb-3">
          <button class="btn btn-success" @click="isOpen = !isOpen" >Add</button>
        </header>

        <b-table
            hover
            :items="employers"
            :fields="fields"
            responsive="sm"
            label-sort-asc=""
            label-sort-desc=""
            label-sort-clear=""
            class="apper__item text-white"
        >
          <template v-slot:cell(actions)="{ item }" >
            <div class="d-flex align-items-center justify-content-center">
              <button
                  type="button"
                  class="btn btn-success me-2"
                  @click="editItem(item)"
              >
                Edit
              </button>
              <button
                  type="button"
                  class="btn btn-danger"
                  @click="deleteItem(item)"
              >
                Del
              </button>
            </div>
          </template>
        </b-table>
      </div>

    </div>
  </div>
</template>

<script>
import BgVideo from "@/components/bgVideo";
import Modal from "@/components/actionModals";
export default {
  name: 'App',
  components: {
    BgVideo, Modal
  },
  data() {
    return {
      fields: [
        { key: 'last_name', sortable: true},
        { key: 'first_name', sortable: true},
        { key: 'age', sortable: true },
        { key: 'last_work_place', sortable: true},
        { key: 'actions'},
      ],
      employers: [],
      isOpen: false,
      isEdit: false,
      selectedEmployee: {}
    }
  },
  created() {
    const employee = localStorage.getItem('employee')
    if (employee) {
      this.employers = JSON.parse(employee)
    }
  },
  methods: {
    handleAdd(form) {
       if (form.id) {
        this.editEmployers(form)
      }
      else  this.addEmployers(form)
    },
    addEmployers(form) {
      this.employers.push(
          {
            first_name: form.name,
            last_name: form.last_name,
            age: form.age,
            last_work_place: form.last_work_place
          }
      )
      for (let i = 1; i <= this.employers.length; i++) {
        this.employers[i - 1].id = i
      }
      localStorage.setItem('employee', JSON.stringify(this.employers))
    },
    editEmployers(form) {
      for (let i = 0; i < this.employers.length; i++) {
        if (this.employers[i].id === form.id) {
          this.employers[i].first_name = form.name
          this.employers[i].last_name = form.last_name
          this.employers[i].age = form.age
          this.employers[i].last_work_place = form.last_work_place
        }
      }
      localStorage.setItem('employee', JSON.stringify(this.employers))
    },
    editItem(item) {
      this.selectedEmployee = item;
      this.isEdit = true
    },
    closeModal() {
      this.isOpen = false
      this.isEdit = false
    },
    deleteItem(item) {
      const id = this.employers.indexOf(item)
      this.employers.splice(id, 1)
      localStorage.setItem('employee', JSON.stringify(this.employers))
    }
  }
}
</script>

<style>
</style>
