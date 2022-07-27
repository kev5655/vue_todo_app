



<template>
  <div class="flex justify-between items-center p-2" 
    :class="{
        'bg-[#2a9d8f]': this.todo.done,
        'bg-[#e76f51]': !this.todo.done
      }">

    <h1 class='text-lg cursor-pointer' 
      @click="toggleIndex">

      {{ todo.todo }}

    </h1>

    <button class="text-lg rounded-xl 
          bg-gray-400 p-1 m-2 text-white"
          @click="removeTodo">
      Delete Todo
    </button>

  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Todos',
  props: ["todoProp", "todoIndex"],
  data() { 
    return {
      todo: this.todoProp,
    }
  },
  methods: {
    toggleIndex() {
      this.$emit("toggleDone-index", this.todoIndex)
    },
     removeTodo() {
      this.$emit("removeTodo-index", this.todoIndex)
     }
  },
}
</script>

