<template>
  <input type="text" v-model="myTodo" />
  <button @click="addTodo">Add Todo</button>
  <div v-if="!isEmpty">
    <p v-for="(todo, index) in todos" :key="index">
      {{ index }}. {{ todo }} <button @click="removeTodo(index)">delete</button>
    </p>
  </div>
  <div v-else>No todos found</div>
</template>

<script>
import { computed, ref } from "vue";
import { useMainStore } from "./store.js";
export default {
  setup() {
    const main = useMainStore();
    const myTodo = ref("");
    const addTodo = () => {
      if (myTodo.value != "") {
        main.addTodo(myTodo.value);
        myTodo.value = "";
      }
    };
    return {
      addTodo,
      myTodo,
      todos: computed(() => main.getAllTodos),
      isEmpty: computed(() => main.todoEmpty),
      removeTodo: main.removeTodo,
    };
  },
};
</script>