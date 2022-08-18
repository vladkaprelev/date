<template>
  <CalendarWrap title="Vue functional calendar">
    <functional-calendar
      v-model="date"
      :is-auto-closeable="true"
      :is-date-range="true"
      :isModal="true"
      :is-multiple="true"
      :newCurrentDate="new Date()"
      ref="calendar"
      :calendars-count="2"
      :limits="{ min: '', max: maxDate }"
      :date-format="'dd.mm.yyyy'"
      placeholder="Период"
      :isLayoutExpandable="false"
    >
      <template v-slot:dateRangeInputs="props">
        <CalendarInput :value="dateFormatFC(props)" @clear="clearDate" />
      </template>
      <template v-slot:navigationArrowLeft> <IconLeft /></template>
      <template v-slot:navigationArrowRight> <IconRight /></template>
    </functional-calendar>
  </CalendarWrap>
</template>

<script lang="ts">
import Vue from "vue";
import CalendarWrap from "@/components/CalendarWrap.vue";
import CalendarInput from "@/components/CalendarInput.vue";
import FunctionalCalendar from "vue-functional-calendar";
import IconLeft from "@/components/IconLeft.vue";
import IconRight from "@/components/IconRight.vue";

Vue.use(FunctionalCalendar, {
  dayNames: ["Пн", "Вт", "Ср", "Чт", "Пт", "Сб", "Вс"],
  monthNames: [
    "Янв",
    "Фев",
    "Мар",
    "Апр",
    "Май",
    "Июн",
    "Июл",
    "Авг",
    "Сен",
    "Окт",
    "Ноя",
    "Дек",
  ],
});
export default Vue.extend({
  name: "FuncCalendar",
  components: { IconRight, IconLeft, CalendarInput, CalendarWrap },
  props: {
    maxDate: {
      type: String,
      default: "18.08.2022",
    },
  },
  data() {
    return {
      date: { startDate: null, endDate: null },
    };
  },
  mounted() {
    this.$refs.calendar.PreMonth();
  },
  methods: {
    clearDate() {
      this.date = { startDate: null, endDate: null };
    },
    dateFormatFC(input) {
      if (input.startDate.length && input.endDate.length) {
        return `${input.startDate} - ${input.endDate}`;
      } else {
        return "";
      }
    },
  },
});
</script>

<style scoped lang="scss">
::v-deep {
  .vfc-main-container {
    width: 552px;
    z-index: 100;
  }
  .vfc-week .vfc-day span.vfc-span-day.vfc-marked {
    background: transparent;
  }
  .vfc-week .vfc-day .vfc-base-start {
    width: 100% !important;
    border-radius: 8px 0px 0px 8px !important;
    background: #1588e2;
  }
  .vfc-week .vfc-day .vfc-base-end {
    width: 100% !important;
    border-radius: 0px 8px 8px 0px !important;
    background: #1588e2;
  }
  .vfc-navigation-buttons,
  .vfc-separately-navigation-buttons {
    margin-top: 8px;
  }
}
</style>
