<template>
    <div class="custom-date">

        <input
          ref="dateInput"
          type="text"
          :value="formattedDate"
          @focus="renderDayPicker"
          @change="onDateChange"
        />
     
     <transition name="slide-fade">
      <div v-if="showDropdown">
        <DayPicker v-if="showDayPicker" @datePicked="renderMonthPicker" />
        <MonthPicker
          v-if="showMonthPicker"
          :date="date"
          @monthPicked="renderYearPicker"
        />
        <YearPicker v-if="showYearPicker" @yearPicked="onDatePicked" />
      </div>
      </transition>
    </div>
</template>

<script>
import DayPicker from "./DayPicker.vue";
import MonthPicker from "./MonthPicker.vue";
import YearPicker from "./YearPicker.vue";


const DatePicker = {
   props: ['formatDate','showToday'],
  data() {
    return {
      showDayPicker: false,
      showMonthPicker: false,
      showYearPicker: false,
      showDropdown: false,
      month: "",
      year: "",
      formattedDate: ''
    };
  },
  components: { DayPicker, MonthPicker, YearPicker },

  mounted() {
    this.resetDate();
  },

  methods: {
    resetDate() {
    let today = new Date();
    let _date = this.showToday ? today.getDate() : "DD";
    this.month = this.showToday ? today.getMonth() + 1 : "MM";
    this.year = this.showToday ? today.getFullYear() : "YYYY";
    this.formattedDate =  `${_date}/${this.month}/${this.year}`;
    },

    renderDayPicker() {
      this.showDayPicker = true;
      this.showDropdown = true;
      this.showYearPicker = false;
      this.showMonthPicker = false;
    },

    renderMonthPicker(d) {
      const _date = d.toString().padStart(2, "0");
      this.showDayPicker = false;
      this.showMonthPicker = true;
      this.showYearPicker = false;
      this.date = _date;
      this.formattedDate = `${_date}/${this.month}/${this.year}`;
    },

    renderYearPicker(m) {
      const _month = m.toString().padStart(2, "0");
        this.showMonthPicker = false
         this.showDayPicker = false;
        this.showYearPicker = true
        this.month = _month,
        this.formattedDate = `${this.date}/${_month}/${this.year}`;
    },

    onDatePicked(y) {
      this.showDropdown = false
      this.showYearPicker = false
      this.year = y,
      this.formattedDate = `${this.date}/${this.month}/${y}`;
    },

    onDateChange(e) {
      const _value = e.target.value;

      const [_date, _month, _year] = _value.split("/"); 
      const showMonth = _value.indexOf("/") >= 1;
      const showYear = _value.lastIndexOf("/") >= 3;

      if (showMonth) {
        this.renderMonthPicker(_date);
      }

      if (showYear) {
        this.showMonthPicker = false,
          this.showYearPicker = true,
          this.month = _month;
      }

      if (_year && _year.length === 4) {
        (this.showDropdown = false), (this.showYearPicker = false);
      }

      this.formattedDate = _value;
    },
  },
};
export default DatePicker;
</script>
<style  scoped>
.custom-date {
  background: white;
  max-width: 300px;
  margin: 1em auto;
  max-height: 300px;
  overflow: hidden;
  border-radius: 4px;
  border: 1px solid #ddd;
}
input {
  border: none;
  font-weight: bold;
  font-size: 1em;
  cursor: pointer;
  color: #555;
  width: 100%;
  background: none;
  text-align: center;
  height: 40px;

}
 .focus-visible {
    border:none;
    outline: none;
  }
  

</style>
