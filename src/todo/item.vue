<template>
  <div :class="['todo-item',todo.completed? 'completed':'']">
      <input 
        type="checkbox"
        class="toggle"
        v-model="todo.completed"
      >
      <label>{{todo.content}}</label>
      <button class="delete" @click="deleteTodo">X</button>
  </div>
</template>
<script>
export default {
  props: {
      todo: {
          type: Object,
          required: true,
      }
  },
  methods: {
      deleteTodo(){
          this.$emit('del', this.todo.id)
      }
  }
}
</script>

<style lang="stylus" scoped>
    .todo-item
        width 100%
        margin 0 auto
        height 50px
        border-bottom 1px solid #000
        text-align left
        line-height 50px
        background-color #fff
        
        input
            width 40px
            height  40px
            border-radius 50%
            background-color #fff
            float left
            border 0
            cursor pointer
            
        label 
            line-height 50px
            height 50px
            display inline-block
            float left
        button 
            width 40px
            height 40px
            float right
            margin-top 5px
            border 0
            background #fff
            display none
            font-size 20px
    .completed
        label 
            text-decoration   line-through
    .todo-item:hover
        button 
            display block
            cursor pointer

</style>
