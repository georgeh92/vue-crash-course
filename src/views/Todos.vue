<template>
  <div>
  	<h2>Todo application</h2>
	<router-link to="/">Home</router-link>
	<hr />
    <AddTodo
      @add-todo='addTodo'
     />
    <TodoList
	    v-if="todos.length"
	    v-bind:todos='todos'
	    v-on:remove-todo="removeTodo"
     />
     <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
export default {
  name: 'app',
  data() {
    return {
      todos: []
    }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {this.todos = json})
  },
  methods:{
      removeTodo(id){
          this.todos = this.todos.filter(t=> t.id !== id)
      },
      addTodo (todo) {
        this.todos.push(todo)
      }
  },
  components: {
    TodoList, AddTodo
  }
}
</script>

<style>

</style>
