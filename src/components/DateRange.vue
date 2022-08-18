<template>
  <CalendarWrap title="Vue2 date range picker">
    <date-range-picker
      v-model="date"
      :max-date="maxDate"
      :auto-apply="true"
      :showDropdowns="true"
      :localeData="localeData"
      :ranges="null"
    >
      <template v-slot:input="props">
        <CalendarInput :value="dateFormat(props)" @clear="clearDate" />
      </template>
    </date-range-picker>
  </CalendarWrap>
</template>

<script lang="ts">
import Vue from "vue";
import CalendarWrap from "@/components/CalendarWrap.vue";
import CalendarInput from "@/components/CalendarInput.vue";
import { format } from "date-fns";
import DateRangePicker from "vue2-daterange-picker";
import "vue2-daterange-picker/dist/vue2-daterange-picker.css";

export default Vue.extend({
  name: "DateRange",
  components: { CalendarInput, CalendarWrap, DateRangePicker },
  props: {
    maxDate: {
      type: Date,
      default: () => new Date(),
    },
  },
  data() {
    return {
      date: { startDate: null, endDate: null },
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
  methods: {
    clearDate() {
      this.date = { startDate: null, endDate: null };
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
  },
});
</script>

<style scoped lang="scss">
::v-deep {
  .daterangepicker.show-ranges {
    width: auto;
  }

  .text-black {
    color: #000;
  }
  .reportrange-text {
    padding: 0;
    border: none;
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
  }
  .daterangepicker td.in-range {
    background: #d8eeff;
  }
  .daterangepicker td.active,
  .daterangepicker td.active:hover {
    background: #1588e2;
  }

  .daterangepicker td.off,
  .daterangepicker td.off.end-date,
  .daterangepicker td.off.in-range,
  .daterangepicker td.off.start-date {
    background: transparent;
  }
}
</style>
