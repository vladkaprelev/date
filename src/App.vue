<template>
  <div id="app">
    <DefaultPicker />
    <VCalendar />
    <FuncCalendar />
    <DateRange />
  </div>
</template>

<script lang="ts">
import Vue from "vue";

import VCalendar from "@/components/VCalendar.vue";
import FuncCalendar from "@/components/VueFuncCalendar.vue";
import DefaultPicker from "@/components/DefaultPicker.vue";
import DateRange from "@/components/DateRange.vue";

export default Vue.extend({
  name: "App",
  components: {
    DateRange,
    DefaultPicker,
    FuncCalendar,
    VCalendar,
  },
  data() {
    return {};
  },

  methods: {},
});
</script>

<style lang="scss">
body {
  margin: 0;
}

* {
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  display: flex;
  flex-wrap: wrap;
}
</style>
