<template>
  <div>
    <div class="todo-item">
      <label>
        <div :class="{ done: todoItem.completed }">
          <input
            type="checkbox"
            :checked="todoItem.completed"
            @click="$emit('changeState', $event)"
          />
          {{ todoItem.content }}
        </div>
        <div class="delete" @click="$emit('delete', todoItem.content)">
          删除
        </div>
        <span class="check-button"></span>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todoItem: Object,
  },
  setup() {},
};
</script>

<style lang="less" scoped>
.todo-item {
  background-color: white;
  padding: 16px;
  border-radius: 8px;
  color: #626262;
  label {
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    span.check-button {
      position: absolute;
      top: 0;
    }
    span.check-button::before,
    span.check-button::after {
      content: "";
      display: block;
      position: absolute;
      width: 18px;
      height: 18px;
      border-radius: 50%;
    }
    span.check-button::before {
      border: 1px solid #b382f9;
    }

    span.check-button::after {
      transition: 0.4s;
      background: #b382f9;
      opacity: 0;
      transform: translate(1px, 1px) scale(0.8);
    }
    .delete {
      float: right;
      color: red;
      font-size: 14px;
      cursor: pointer;
    }
  }

  input {
    margin-right: 16px;
    opacity: 0;
  }
  input:checked + span.check-button::after {
    opacity: 1;
  }
}

.done {
  text-decoration: line-through;
  font-style: italic;
}
</style>
