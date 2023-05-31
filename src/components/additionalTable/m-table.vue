<template>
  <div>
    <b-table
        hover
        :items="addressData"
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
      v-if="isOpen"
      :editedAddress="editedAddress"
      @closeM2="closeM2"
      @formData="handleFormData"
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
    editedIndex: Number,
  },
  data() {
    return {
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
      addressData: [...this.address],
      editedAddressIndex: -1,
      editedAddress: {
          country: '',
          street: '',
          village: '',
      },
      defaultAddress: {
        country: '',
        street: '',
        village: '',
      },
      isOpen: false,
    }
  },
  computed: {

  },
  methods: {
    handleFormData(formData) {
      if (this.editedAddressIndex > -1) {
        Object.assign(this.addressData[this.editedAddressIndex], formData)
      } else {
        this.addressData.push(formData)
      }
      this.$emit('newAddress', this.addressData)
    },
    edit(item) {
      this.isOpen = true
      this.editedAddressIndex = this.addressData.indexOf(item)
      this.editedAddress = Object.assign({}, item)
    },
    del(item) {
      this.editedAddressIndex = this.addressData.indexOf(item)
      this.addressData.splice(this.editedAddressIndex, 1)
      this.$emit('deletedAddress', this.addressData)
    },
    closeM2() {
      this.isOpen = false
      this.$nextTick(() => {
        this.editedEmployers = Object.assign({}, this.defaultAddress)
        this.editedAddressIndex = -1
      })
    },
  },
}
</script>

<style scoped>

</style>