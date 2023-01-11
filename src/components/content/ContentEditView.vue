<template>
    <div>
      {{editTitle}}
      <div>
        <input type="text" v-model="editTitle" @keyup.enter="onEditDone">
        <button class="btn" @click="onEditDone">수정완료</button>
      </div>
    </div>
</template>

<script>
export default {
  props: {
    changeContent:{
      type: Object
    }
  },

  data(){
    return{
      editTitle: '',
      completed: false
    }
  },methods: {
    onEditDone(){
      console.log('자식')
      this.completed = true
      this.$emit('onEditDone', this.editTitle, this.completed)
    }
  },
  mounted(){
    console.log('this.changeContent:', this.changeContent.title)
  }
}
</script>

<style>

</style>