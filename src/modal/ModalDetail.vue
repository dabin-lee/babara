<template>
  <div class="modalBody">
    <div class="modal-cont">
      <h5>{{ item.title }}</h5>
      <p>{{ item.description }}</p>
      <ul class="d-flex flex-row">
        <li v-for="(img, index) in item.images" :key="index">
          <img :src="img" alt="" style="width: 40px; height: 30px" />
        </li>
      </ul>
      <button @click="closeModal">close</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "modal-detail",
  props: {
    item: {
      type: Object,
    },
  },
  data() {
    return {
      imgList: [],
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    },
  },
  mounted(){
    console.log(this.item)
  }
};
</script>

<style>
.modalBody {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.3);
}
.modal-cont {
  width: 300px;
  padding: 20px;
  background-color: #fff;
}
</style>
