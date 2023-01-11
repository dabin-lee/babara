<template>
    <div>
      <p v-if="!edit">{{ product.title }}</p>
      <div v-else>
        <input type="text" v-model="newTitle">
        <button class="btn" @click="changeTitle">수정완료</button>
      </div>
        <button @click="this.edit = !this.edit" v-show="!this.edit">수정</button>

    </div>
</template>

<script>
export default {
  props: {
    product:{
      type: Object
    }
  },

  data(){
    return{
      edit: false,
      newTitle: ''
    }
  },methods: {
    changeTitle(){
      this.$emit("changeTitle", this.newTitle, this.product.id)
    },
    openEditBox(){

    }
  },
  mounted(){
    // console.log('this.changeContent:', this.changeContent.title)
  }
}
</script>

<style>

</style>