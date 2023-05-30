<template>
  <div class="wrapper">

    <bg-video />

    <Modal
        :selectedEmployee="selectedEmployee"
        v-if="isOpen || isEdit"
        @close_modal="closeModal"
        @added-employee="addEmployers"
        :isOpen="isOpen"
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
    addEmployers(employersForm) {

      employersForm.id = this.employers.length + 1;

      this.employers.push(
          {
            id: employersForm.id,
            first_name: employersForm.name,
            last_name: employersForm.last_name,
            age: employersForm.age,
            last_work_place: employersForm.last_work_place,
            subForm: employersForm.subForm
          }
      )

      console.log('success adding', this.employers)

      localStorage.setItem('employee', JSON.stringify(this.employers))
    },

    editEmployers(form) {
      for (let i = 0; i < this.employers.length; i++) {
        if (this.employers[i].id === form.id) {
          this.employers[i].first_name = form.name
          this.employers[i].last_name = form.last_name
          this.employers[i].age = form.age
          this.employers[i].last_work_place = form.last_work_place
          this.employers[i].id = form.id

          // for (let j = 0; j < this.employers[i].subForm.length; j++) {
          //   this.employers[i].subForm[j].name = form.subForm.name
          //   this.employers[i].subForm[j].type = form.subForm.type
          //   this.employers[i].subForm[j].material = form.subForm.material
          //   this.employers[i].subForm[j].selected = form.subForm.selected
          //   this.employers[i].subForm[j].selectDate = form.subForm.selectDate
          //   this.employers[i].subForm[j].byDefaultColor = form.subForm.byDefaultColor
          //   this.employers[i].subForm[j].quantity = form.subForm.quantity
          //   this.employers[i].subForm[j].quantity = form.subForm.quantity
          //   this.employers[i].subForm[j].id = form.subForm.id
          //
          // }
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
