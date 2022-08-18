<template>
  <div class="picker-block">
    <h2 class="title">{{ title }}</h2>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "CalendarWrap",
  props: {
    title: {
      type: String,
      default: "",
    },
  },
};
</script>

<style scoped lang="scss">
.picker-block {
  width: 50%;
  display: flex;
  flex-flow: column;
  padding: 20px;
  border: 1px solid #2c3e50;
}
</style>
