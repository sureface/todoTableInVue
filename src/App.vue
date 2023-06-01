<template>
  <div class="wrapper">

    <bg-video />

    <Modal
        v-if="isOpen"
        :editedIndex="editedIndex"
        :editedEmployers="editedEmployers"
        @close_modal="closeModal"
        @formData="handleFormData"
    />

    <div class="container">

      <div class="text-center mt-5 mb-5 text-secondary h2 text-uppercase">
        list of Employers to Google
      </div>

      <div class="apper">

        <header class="mb-3">
          <button class="btn btn-success" @click="isOpen = !isOpen">Add</button>
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
        { key: 'name', sortable: true},
        { key: 'last_name', sortable: true},
        { key: 'age', sortable: true },
        { key: 'last_work_place', sortable: true},
        { key: 'actions'},
      ],
      employers: [],
      editedIndex: -1,
      editedEmployers: {
        name: '',
        last_name: '',
        age: 0,
        last_work_place: '',
        address: [
          {
            country: '',
            street: '',
            village: '',
          }
        ]
      },
      defaultEmployers: {
        name: '',
        last_name: '',
        age: 0,
        last_work_place: '',
        address: [
          {
            country: '',
            street: '',
            village: '',
          }
        ]
      },
      isOpen: false,
    }
  },
  created() {
    this.initialize();
  },
  methods: {
    initialize() {
      this.employers = [
        {
          name: 'joseph',
          last_name: 'josephev',
          age: '33',
          last_work_place: 'Google',
          address: [
            {
              country: 'USA',
              street: 'Street 77',
              village: 'silicon',
            },
            {
              country: 'USA',
              street: 'Street 77',
              village: 'silicon',
            },
          ]
        },
        {
          name: 'joseph',
          last_name: 'josephev',
          age: '33',
          last_work_place: 'Google',
          address: [
            {
              country: 'USA',
              street: 'Street 77',
              village: 'silicon',
            },
            {
              country: 'USA',
              street: 'Street 77',
              village: 'silicon',
            },
          ]
        },
        {
          name: 'joseph',
          last_name: 'josephev',
          age: '33',
          last_work_place: 'Google',
          address: [
            {
              country: 'USA',
              street: 'Street 77',
              village: 'silicon',
            },
            {
              country: 'USA',
              street: 'Street 77',
              village: 'silicon',
            },
          ]
        },
        {
          name: 'joseph',
          last_name: 'josephev',
          age: '33',
          last_work_place: 'Google',
          address: [
            {
              country: 'USA',
              street: 'Street 77',
              village: 'silicon',
            },
            {
              country: 'USA',
              street: 'Street 77',
              village: 'silicon',
            },
          ]
        },
        {
          name: 'joseph',
          last_name: 'josephev',
          age: '33',
          last_work_place: 'Google',
          address: [
            {
              country: 'USA',
              street: 'Street 77',
              village: 'silicon',
            },
            {
              country: 'USA',
              street: 'Street 77',
              village: 'silicon',
            },
          ]
        },
      ]
    },
    handleFormData(formData) {
      if (this.editedIndex > -1) {
        Object.assign(this.employers[this.editedIndex], formData)
      } else {
        this.employers.push(formData)
      }
    },
    editItem(item) {
      this.isOpen = true
      this.editedIndex = this.employers.indexOf(item)
      this.editedEmployers = Object.assign({}, item)
    },
    closeModal() {
      this.isOpen = false
      this.$nextTick(() => {
        this.editedEmployers = Object.assign({}, this.defaultEmployers)
        this.editedIndex = -1
      })
    },
    deleteItem(item) {
      this.editedIndex = this.employers.indexOf(item)
      this.employers.splice(this.editedIndex, 1)
    }
  }
}
</script>

<style>
</style>
