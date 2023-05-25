<template>
  <div>
    <b-table
        hover
        :items="products"
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
      v-if="isOpenM2"
      :selectedProducts="selectedProducts"
      @added-products="handleAdd"
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
    m2Products: Array,
  },
  data() {
    return {
      products: [],
      fields: [
        {
          key: 'name',
          sortable: true,
        },
        {
          key: 'material',
          sortable: true,
        },
        {
          key: 'type',
          sortable: true,
        },
        {
          key: 'actions',
        },
      ],
      isOpenM2: false,
      selectedProducts: {}
    }
  },
  created() {
    this.products = this.m2Products;
  },
  methods: {
    handleAdd(form) {
      for (let i = 0; i < this.products.length; i++) {
        if (this.products[i].id === form.id) {
          this.products[i].name = form.name
          this.products[i].type = form.type
          this.products[i].material = form.material
        }
      }
    },
    edit(item) {
      this.selectedProducts = item;
      this.isOpenM2 = true;
    },
    del(item) {
      const id = this.products.indexOf(item)
      this.products.splice(id, 1)
    },
    closeM2() {
      this.isOpenM2 = false
    }
  },

}
</script>

<style scoped>

</style>