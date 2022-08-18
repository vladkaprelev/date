<template>
  <div id="app">
    <div class="picker-block">
      <h2 class="title">Текущий пикер</h2>
      <date-picker
        v-model="time1"
        valueType="format"
        range
        :disabled-date="disabledDate"
      ></date-picker>
    </div>

    <div class="picker-block">
      <h2 class="title">V-Calendar</h2>
      <v-date-picker
        class="inline-block h-full"
        v-model="date"
        is-range
        :columns="2"
        :max-date="new Date()"
      >
        <template v-slot="{ inputValue, togglePopover }">
          <div class="input-block">
            <input
              placeholder="Период"
              class="date-input"
              @click="togglePopover()"
              :value="dateFormatVS(inputValue.start, inputValue.end)"
              readonly
            />
            <button @click.stop="clearVC" class="clear"></button>
          </div>
        </template>
      </v-date-picker>
    </div>

    <div class="picker-block">
      <h2 class="title">Vue functional calendar</h2>
      <functional-calendar
        v-model="calendarData"
        :is-modal="true"
        :is-date-range="true"
        :is-multiple="true"
        :isAutoCloseable="true"
        @opened="opened"
        ref="calendar"
        :calendars-count="2"
        :limits="{ min: '', max: '16.08.2022' }"
        :date-format="'dd.mm.yyyy'"
        placeholder="Период"
        :isLayoutExpandable="true"
      >
        <template slot="navigationArrowRight">
          123
          <!--          <div class="input-block">-->
          <!--            <input-->
          <!--              placeholder="Период"-->
          <!--              :value="dateFormatFC(props)"-->
          <!--              class="date-input"-->
          <!--              readonly-->
          <!--            />-->
          <!--          </div>-->
        </template>
      </functional-calendar>
      <button @click.stop="clearFC">clear</button>
    </div>

    <div class="picker-block">
      <h2 class="title">Vue2 date range picker</h2>
      <date-range-picker
        v-model="dateRange"
        :max-date="new Date()"
        :auto-apply="true"
        :showDropdowns="true"
        :localeData="localeData"
      >
        <!--    header slot-->
        <template #input="input">
          <div class="input-block">
            <input
              type="text"
              class="date-input"
              placeholder="Период"
              :value="dateFormat(input)"
              readonly
            />
            <button @click.stop="clearDR" class="clear"></button>
          </div>
        </template>
        <div slot="header" class="slot"></div>
        <div slot="footer" class="slot"></div>
        <div slot="ranges" class="slot"></div>
      </date-range-picker>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import DatePicker from "vue2-datepicker";
import VCalendar from "v-calendar";
import "vue2-datepicker/index.css";
import FunctionalCalendar from "vue-functional-calendar";

Vue.use(FunctionalCalendar, {
  dayNames: ["Mo", "Tu", "We", "Th", "Fr", "Sa", "Su"],
});
Vue.use(VCalendar);
import DateRangePicker from "vue2-daterange-picker";
//you need to import the CSS manually
import "vue2-daterange-picker/dist/vue2-daterange-picker.css";

import { format } from "date-fns";

export default Vue.extend({
  name: "App",
  components: { DatePicker, DateRangePicker },
  data() {
    return {
      time1: null,
      date: { start: "", end: "" },
      dateRange: { startDate: null, endDate: null },
      calendarData: { startDate: null, endDate: null },
      localeData: {
        direction: "ltr",
        format: "dd.mm.yyyy",
        separator: " - ",
        applyLabel: "Apply",
        cancelLabel: "Cancel",
        weekLabel: "W",
        customRangeLabel: "Custom Range",
        daysOfWeek: ["Пн", "Вт", "Ср", "Чт", "Пт", "Сб", "Вс"],
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
        firstDay: 0,
      },
    };
  },
  mounted() {
    this.$refs.calendar.PreMonth();
  },
  methods: {
    clearVC() {
      this.date = { start: "", end: "" };
    },
    clearDR() {
      this.dateRange = { startDate: null, endDate: null };
    },
    clearFC() {
      this.calendarData = { startDate: null, endDate: null };
      console.log(this.calendarData);
    },
    disabledDate(date) {
      return date > new Date();
    },
    dateFormatVS(start, end) {
      if (start && end) {
        return `${start} - ${end}`;
      } else {
        return "";
      }
    },
    dateFormat(input) {
      if (input.startDate && input.endDate) {
        return `${format(input.startDate, "dd.MM.yyyy")} - ${format(
          input.endDate,
          "dd.MM.yyyy"
        )}`;
      } else {
        return "";
      }
    },
    opened() {
      console.log("open");
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

  .date-input {
    padding: 11px 16px;
    width: 275px;
    background: #ffffff;
    border: 1px solid #d6d6d6;
    border-radius: 12px;
    text-align: start;
  }
}

.slot {
  color: white;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.daterangepicker.show-ranges {
  width: auto;
}

.text-black {
  color: #000;
}

.picker-block {
  flex: 1 0 45%;
  padding: 20px;
  border-bottom: 1px solid #2c3e50;
  border-left: 1px solid #2c3e50;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
}

.vue-daterange-picker {
  .reportrange-text {
    padding: 0;
    border: none;
  }

  .daterangepicker {
    &:after,
    &:before {
      display: none;
    }

    &.show-ranges {
      width: auto;
      min-width: auto;
    }
  }

  .slot {
    display: none;
  }
}

.input-block {
  display: flex;
  align-items: center;
  position: relative;
}

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
.vc-highlight {
  width: 36px !important;
  height: 36px !important;
  background: #1588e2 !important;
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
</style>
