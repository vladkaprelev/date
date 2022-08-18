<template>
  <CalendarWrap title="Текущий пикер">
    <date-picker
      v-model="time1"
      valueType="format"
      range
      :disabled-date="disabledDate"
    ></date-picker>
  </CalendarWrap>
</template>

<script lang="ts">
import Vue from "vue";
import DatePicker from "vue2-datepicker";
import "vue2-datepicker/index.css";
import CalendarWrap from "@/components/CalendarWrap.vue";
export default Vue.extend({
  name: "DefaultPicker",
  components: { CalendarWrap, DatePicker },

  data() {
    return {
      time1: null,
    };
  },
  methods: {
    disabledDate(date) {
      return date > new Date();
    },
  },
});
</script>

<style scoped lang="scss">
.vfc-single-input,
.vfc-multiple-input input {
}
</style>
