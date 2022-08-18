<template>
  <CalendarWrap title="V-Calendar">
    <v-date-picker
      class="inline-block h-full"
      :masks="masks"
      v-model="date"
      is-range
      :columns="2"
      :max-date="maxDate"
    >
      <template v-slot="{ inputValue, togglePopover }">
        <CalendarInput
          :value="dateFormatVS(inputValue.start, inputValue.end)"
          @clickInput="togglePopover()"
          @clear="clearDate"
        />
      </template>
      <template slot="header-left-button"><IconLeft /></template>
      <template slot="header-right-button"><IconRight /></template>
    </v-date-picker>
  </CalendarWrap>
</template>

<script lang="ts">
import Vue from "vue";
import CalendarWrap from "@/components/CalendarWrap.vue";
import VCalendar from "v-calendar";
import CalendarInput from "@/components/CalendarInput.vue";
import IconLeft from "@/components/IconLeft.vue";
import IconRight from "@/components/IconRight.vue";

Vue.use(VCalendar);

export default Vue.extend({
  name: "VCalendar",
  components: { IconRight, IconLeft, CalendarInput, CalendarWrap },
  props: {
    maxDate: {
      type: Date,
      default() {
        return new Date();
      },
    },
  },
  data() {
    return {
      date: { start: "", end: "" },
      masks: {
        title: "MMMM YYYY",
        weekdays: "WW",
        navMonths: "MMM",
        input: ["L", "DD.MM.YYY", "YYYY/MM/DD"],
        dayPopover: "WWW, MMM D, YYYY",
        data: ["L", "DD.MM.YYY", "YYYY/MM/DD"],
      },
    };
  },
  methods: {
    clearDate() {
      this.date = { start: "", end: "" };
    },
    dateFormatVS(start, end) {
      if (start && end) {
        return `${start} - ${end}`;
      } else {
        return "";
      }
    },
  },
});
</script>

<style scoped lang="scss">
::v-deep {
  .vc-arrows-container {
    top: 6px;
  }
  .vc-day,
  .vc-day-content {
    width: 36px;
    height: 36px;
    &:focus {
      background: transparent;
    }
    &:hover {
      background: transparent;
    }
  }
  .vc-popover-caret {
    display: none;
  }
  .vc-highlight {
    width: 36px !important;
    height: 36px !important;
    background: #1588e2 !important;
    border: none !important;

    &.vc-highlight-base-start {
      background: #1588e2 !important;
    }
    &.vc-highlight-base-end {
      width: 50% !important;
      border-radius: 0 !important;
      border-left-width: 0 !important;
      background: #1588e2 !important;
    }
    &.vc-highlight-base-middle {
      background: #d8eeff !important;
    }
  }
}
</style>
