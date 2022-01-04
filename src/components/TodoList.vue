<template>
  <div class="todo-list">
    <todo-list-item
      v-for="todo in todos"
      :key="todo.id"
      :todoItem="todo"
      @changeState="todo.completed = $event.target.checked"
      @delete="deleteItem"
    />
  </div>
</template>

<script>
import TodoListItem from "./TodoListItem.vue";
export default {
  components: {
    TodoListItem,
  },
  props: {
    todos: Array,
  },
  setup(props, ctx) {
    const deleteItem = (content) => {
      ctx.emit("deleteItem", content);
    };
    return {
      deleteItem,
    };
  },
};
</script>

<style lang="less" scoped>
.todo-list {
  display: grid;
  row-gap: 14px;
}
</style>
