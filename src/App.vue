<template>
  <div class="bg-gray-600 border-gray-600 
              rounded-t-xl text-white 
              w-1/2 m-auto mt-12">
    <div class="text-center border-b-2 
              border-black py-4">

      <h1 class="text-3xl py-4">Meine Todo's</h1>
      <p v-if="openTodos.length" 
          class="text-xl">
        Offene Todos: {{openTodos.length}} 
      </p>
      <p v-else
          class="text-xl">
        Keine Todos
      </p>

      <form ref="todoForm"
        class="grid grid-cols-3 p-2">
        <input type="text"
          placeholder="Neues Todo..."
          v-model="newTodo"
          class="col-span-2 py-2 pl-3 m-2 rounded-xl
            text-gray-900 bg-gray-400">
        <input type="submit" 
            @click="addTodo" 
            value="Add Todo"
            class="col-span-1 m-2 rounded-xl cursor-pointer
            text-gray-900 bg-gray-400">
      </form>

    </div>

    <div v-for="(todo, index) in todos" :key="todo.todo">
      <Todo :todoProp="todo" 
            :todoIndex="index"
            @toggleDone-index="toggleDone"
            @removeTodo-index="deleteTodo"/>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo.vue'

export default {
  name: 'App',
  data() {
    return {
      newTodo: "",
      todos: [
        {todo: "Einkaufen", done: true},
        {todo: "Sport", done: false},
        {todo: "Programmieren", done: false},
      ],
    }
  },
  methods: {
    toggleDone(index) {
      this.todos[index].done = !this.todos[index].done;
      this.storeTodos()
    },
    deleteTodo(index) {
      this.todos.splice(index, 1)
      this.storeTodos()
    },
    addTodo(){
      if(this.newTodo.trim() == ""){
        return
      }
      this.todos.push({todo: this.newTodo, done: false})
      this.storeTodos()
    },
    storeTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos))
    },
  },
  computed: {
    openTodos() {
      const openTodos = this.todos.filter((todo) => {
        return !todo.done
      })
      return openTodos;
    }
  },
  mounted() {
    let data = localStorage.getItem("todos")
    if(data !== "" && data !== null){
      this.todos = JSON.parse(data)
    } else {
      this.todos = []
    }
  },
  components: {
    Todo
  }
}
</script>

