<template>
  <div class="helper">
      <span class="left">{{unFinishedTodoLength}} items left</span>
      <span class="tabs">
          <span
            v-for="state in states"
            :key="state"
            :class="[state, filter === state ? 'actived': '']"
            @click="toggleFilter(state)"
          >
              {{state}}
          </span>          
      </span>
      <span class="clear" @click="clearAllCompleted">clear completed</span>
  </div>
</template>
<script>
export default {
    props: {
        filter: {
            type: String,
            required: true
        },
        todos: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            states: ['all','active','completed']
        }
    },
    computed: {
        unFinishedTodoLength(){
            return this.todos.filter(todo => !todo.completed).length
        }
    },
    methods:{
        clearAllCompleted(){
            this.$emit('clearAllCompleted')
        },
        toggleFilter(state){
            this.$emit('toggle', state)
        }
    }
}
</script>
<style lang="stylus" scoped>
    .helper
        width 100%
        height 40px
        line-height 40px
        margin 0 auto 
        background #fff
        text-indent 10px
        .left
            float left
        .tabs
            margin-left 100px
            span 
                padding 0 5px
                margin 0 5px
                cursor pointer
            .actived
                border 1px solid #000000


        .clear
            float right
            margin-right  10px
            
</style>
