<template>
  <button @click.stop.self="$emit('clear')" class="clear"></button>
</template>

<script>
export default {
  name: "ClearButton",
  props: {
    title: {
      type: String,
      default: "",
    },
  },
};
</script>

<style scoped lang="scss">
.clear {
  border: none;
  background: transparent;
  outline: none;
  cursor: pointer;
  position: absolute;
  width: 16px;
  height: 16px;
  top: 50%;
  margin-top: -16px;
  right: 15px;
}

.clear:before,
.clear:after {
  position: absolute;
  content: " ";
  height: 16px;
  width: 2px;
  background-color: #333;
}

.clear:before {
  transform: rotate(45deg);
}

.clear:after {
  transform: rotate(-45deg);
}
</style>
