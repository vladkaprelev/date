<template>
  <div class="input-block">
    <input
      placeholder="Период"
      class="date-input"
      @click="$emit('clickInput')"
      :value="value"
      readonly
    />
    <ClearButton @clear="$emit('clear')" />
  </div>
</template>

<script>
import ClearButton from "@/components/ClearButton";
export default {
  name: "CalendarInput",
  components: { ClearButton },
  props: {
    value: {
      type: String,
      default: "",
    },
  },
};
</script>

<style scoped lang="scss">
.input-block {
  display: flex;
  align-items: center;
  position: relative;
  width: 275px;
  .date-input {
    width: 100%;
    padding: 11px 16px;
    background: #ffffff;
    border: 1px solid #d6d6d6;
    border-radius: 12px;
    text-align: start;
    color: #000;
    font-size: 13px;
    font-weight: 400;
    line-height: 16px;
  }
}
</style>
