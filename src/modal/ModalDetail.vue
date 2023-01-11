<template>
  <div class="modal-body">
    <div class="modal-cont">
      <h5>{{ item.title }}</h5>
      <p>{{ item.description }}</p>
      <ul class="d-flex flex-row">
        {{
          item
        }}
        <li v-for="(img, index) in item" :key="index">
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
      type: Array,
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
};
</script>

<style>
.modal-body {
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
