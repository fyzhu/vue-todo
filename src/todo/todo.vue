<template>

    <section class="real-app">
        <input 
            type="text"
            class="add-input"
            autofocus="autofocus"
            placeholder="接下去要做什么？"
            @keyup.enter="addTodo"
        >
        <div class="no-todo" v-if="!filteredTodos.length">暂无任务</div>
        <item 
            :todo="todo"
            v-for="todo in filteredTodos"
            :key="todo.id"
            @del="deleteTodo"
        />        
        <tabs 
            :filter="filter" 
            :todos="todos" 
            @toggle="toggleFilter"
            @clearAllCompleted="clearAllCompleted"
        >
        </tabs>
    </section>
</template>
<script>
import Item from './item.vue'
import Tabs from './tabs.vue'
let id = 0
export default {
    data(){
        return{
            todos:[],
            filter: 'all'
        }
    },
    components: {
        Item,
        Tabs
    },
    computed:{
        filteredTodos(){
            if(this.filter === 'all'){
                return this.todos
            }
            const completed = this.filter === 'completed'
            return this.todos.filter(todo => completed === todo.completed)
        }
    },
    methods: {
      addTodo(e){
          this.todos.unshift({
              id: id ++,
              content: e.target.value.trim(),
              completed: false
          })
          e.target.value=''
      },
      deleteTodo(id){
          this.todos.splice(this.todos.findIndex(todo => todo.id ===id), 1)
      },
      toggleFilter(state){
          this.filter = state
      },
      clearAllCompleted(){
          this.todos= this.todos.filter(todo => !todo.completed)
      }
  }
}
</script>
<style lang="stylus" scoped>
section 
    text-align center
    width 600px
    margin 0 auto
    .no-todo
        background #fff
        height 50px
        line-height 50px
    input
        width 100%
        margin 0 auto
        padding 0
        height 50px
        text-indent 20px
        font-size 20px
        border 0

</style>
