<template>
  <div class="container">
    <h2 v-if="errMessage">{{ errMessage }}</h2>
    <!-- products -->
    <ul class="list-group">
      <li
        v-for="(product, index) in products"
        :key="product.id"
        class="list-group-item d-flex flex-column"
      >
        <div @click="openDetail(index)">
          <h2>{{ product.id }}</h2>
          <img :src="product.thumbnail" alt="" style="width: 100%" />
        </div>
        <content-edit-view :product="product" @changeTitle="doneEdit"/>

        <button
          type="button"
          class="btn btn-primary"
          @click="deleteItem(index)"
        >
          delete
        </button>
      </li>
    </ul>
  </div>
  <modal v-if="modalState" :item="item" @closeModal="closeModal" />
</template>

<script>
import axios from "axios";
import Modal from "@/modal/ModalDetail.vue";
import ContentEditView from './content/ContentEditView.vue';
export default {
  components: { Modal, ContentEditView },
  name: "test-crud",
  data() {
    return {
      products: [],
      errMessage: "",
      itemNum: "",
      modalState: false,
      item: {},
      cloneProducts: [],
    };
  },
  methods: {
    async fetchData() {
      try {
        const dummy = await axios.get(
          "https://dummyjson.com/products?limit=10"
        );
        this.products = dummy.data.products;
        this.cloneProducts = JSON.parse(JSON.stringify(this.products));
      } catch (err) {
        this.errMessage = err.message;
      }
    },
    async deleteItem(index) {
      const id = index + 1;
      this.products.splice(index, 1);
      try {
        await axios.delete(`https://dummyjson.com/products/${id}`);
        this.products = await this.products.filter((item) => item.id !== id);
      } catch (err) {
        this.errMessage = err.message;
      }
      // this.products.splice(index, 1);
    },
    openDetail(id) {
      this.item = this.products[id];
      this.modalState = true;
    },
    closeModal() {
      this.modalState = false;
    },
    deepClone() {
      this.cloneItem = JSON.parse(JSON.stringify(this.products));
    },
    doneEdit(item, id){
      console.log('item', item)
      console.log('id', id)
    }
  },
  mounted() {
    this.fetchData();
  },
  created() {
    // this.cloneItem = _.cloneDeep(this.products);
    // console.log(this.cloneItem);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  max-width: 576px;
}
.deleteItem {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  z-index: 888;
}
</style>
