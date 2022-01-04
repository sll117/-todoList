<template>
  <div class="filters">
    <span
      v-for="obj in state"
      :key="obj.value"
      class="filter"
      :class="{ active: obj.value === clicked }"
      @click="changeState(obj.value)"
      >{{ obj.label }}</span
    >
  </div>
</template>

<script>
export default {
  props: {
    clicked: String,
  },
  setup(props, ctx) {
    const state = [
      {
        label: "全部",
        value: "all",
      },
      {
        label: "已完成",
        value: "done",
      },
      {
        label: "未完成",
        value: "undone",
      },
    ];

    const changeState = (val) => {
      ctx.emit("changeState", val);
    };

    return {
      state,
      changeState,
    };
  },
};
</script>

<style lang="less" scoped>
.filters {
  display: flex;
  margin: 24px 2px;
  color: #c0c2ce;
  font-size: 14px;
  .filter {
    margin-right: 14px;
    transition: 0.8s;
    cursor: pointer;
  }
  .active {
    color: #6b729c;
    transform: scale(1.2);
  }
}
</style>
