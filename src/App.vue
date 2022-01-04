<template>
  <main>
    <div class="container">
      <h1>欢迎使用待办事项!</h1>
      <TodoAdd @addTodo="addTodo" :id="todos.length" />
      <TodoFilter @changeState="changeState" :clicked="clicked" />
      <TodoList :todos="filterTodo" @deleteItem="deleteItem" />
    </div>
  </main>
</template>

<script>
import TodoList from "./components/TodoList.vue";
import TodoAdd from "./components/TodoAdd.vue";
import TodoFilter from "./components/TodoFilter.vue";
import { ref, computed } from "vue";
export default {
  components: { TodoList, TodoAdd, TodoFilter },
  name: "App",
  setup() {
    let { todos, addTodo, deleteItem } = useTodos();
    let { filterTodo, clicked, changeState } = useFilterTodo(todos);
    return {
      todos,
      filterTodo,
      clicked,
      addTodo,
      changeState,
      deleteItem,
    };
  },
};

//todo定义
function useTodos() {
  //所有的todos
  const todos = ref([]);
  const addTodo = (todo) => {
    todos.value.push(todo);
  };
  const deleteItem = (content) => {
    todos.value = todos.value.filter((item) => item.content !== content);
  };
  return {
    todos,
    addTodo,
    deleteItem,
  };
}
//过滤后的todo定义
function useFilterTodo(todos) {
  //当前选择的todo状态
  const clicked = ref("all");
  const changeState = (val) => {
    clicked.value = val;
  };

  const filterTodo = computed(() => {
    if (clicked.value === "all") return todos.value;
    let state = clicked.value === "done";
    return todos.value.filter((item) => item.completed === state);
  });
  return {
    clicked,
    filterTodo,
    changeState,
  };
}
</script>

<style lang="less">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
}

main {
  width: 100vw;
  min-height: 100vh;
  display: grid;
  align-items: center;
  justify-items: center;
  background-color: rgb(203, 210, 240);
}

.container {
  width: 60%;
  max-width: 400px;
  border-radius: 24px;
  padding: 48px 28px;
  background-color: rgb(245, 246, 252);
}

h1 {
  margin: 24px 0;
  font-size: 28px;
  color: #414873;
  text-align: center;
}
</style>
