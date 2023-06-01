<template>
  <div>
    <b-table
        hover
        :items="editedAddress"
        :fields="fields"
        responsive="sm"
        label-sort-asc=""
        label-sort-desc=""
        label-sort-clear=""
        class="product"
    >
      <template v-slot:cell(actions)="{ item }" >
        <div class="d-flex align-items-center justify-content-center">
          <button
              type="button"
              class="btn btn-success me-2"
              @click="edit(item)"
          >
            Edit
          </button>
          <button
              type="button"
              class="btn btn-danger"
              @click="del(item)"
          >
            Del
          </button>
        </div>
      </template>
    </b-table>

    <m-modal
        v-if="m2modal"
        @m2form="getM2Form"
        :editedIndexTable="editedIndexTable"
        :emptyM2="editedIndexTable > -1 ? emptyM2 : this.add"
        @closeM2="closeM2"
    />
  </div>
</template>

<script>
import mModal from './m-modal';
export default {
  name: "m-table",
  components: {
    mModal,
  },
  props: {
    address: Array,
    add: Object
  },
  data() {
    return {
      editedAddress: [...this.address],
      fields: [
        {
          key: 'country',
          sortable: true,
        },
        {
          key: 'street',
          sortable: true,
        },
        {
          key: 'village',
          sortable: true,
        },
        {
          key: 'actions',
        },
      ],
      editedIndexTable: -1,
      emptyM2: {
          country: '',
          village: '',
          street: ''
      },
      m2modal: false
    }
  },
  methods: {
    getM2Form(form) {
      console.log('form', form)
      if (this.editedIndexTable > -1) {
        Object.assign(this.editedAddress[this.editedIndexTable], form)
      } else {
        this.editedAddress.push(form)
      }
    },
    closeM2() {
      this.m2modal = false
    },
    edit(item) {
      this.m2modal = true
      this.editedIndexTable = this.editedAddress.indexOf(item)
      this.emptyM2 = Object.assign({}, item)
    },
    del(item) {
      console.log(1,item)
      this.editedIndexTable = this.editedAddress.indexOf(item)
      this.editedAddress.splice(this.editedIndexTable, 1)
    },
  },
  watch: {
    add: function (newVal) {
      this.editedAddress.push(newVal)
    }
  }
}
</script>

<style scoped>

</style>