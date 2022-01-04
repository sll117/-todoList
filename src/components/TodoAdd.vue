<template>
  <div class="input-add">
    <input type="text" name="todo" v-model="content" @keyup.enter="addTodo" />
    <button @click="addTodo"><i class="plus"></i></button>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  props: {
    id: Number,
  },
  setup(props, context) {
    const content = ref("");
    const addTodo = () => {
      if (!content.value.trim().length) return;
      //传一个对象,包含了item信息
      let obj = {
        content: content.value,
        completed: false,
        id: props.id,
      };
      context.emit("addTodo", obj);
      content.value = "";
    };

    return {
      addTodo,
      content,
    };
  },
};
</script>

<style lang="less" scoped>
.input-add {
  position: relative;
  display: flex;
  align-items: center;
  input {
    padding: 16px 52px 16px 18px;
    border-radius: 48px;
    border: none;
    outline: none;
    width: 100%;
    font-size: 16px;
    color: #626262;
  }
  button {
    width: 46px;
    height: 46px;
    border-radius: 50%;
    background: linear-gradient(#c0a5f3, #7f95f7);
    border: none;
    outline: none;
    color: white;
    position: absolute;
    right: 0px;
    cursor: pointer;
  }

  .plus {
    display: block;
    width: 100%;
    height: 100%;
    background: linear-gradient(#fff, #fff), linear-gradient(#fff, #fff);
    background-repeat: no-repeat;
    background-position: center;
    background-size: 50% 2px, 2px 50%;
  }
}
</style>
