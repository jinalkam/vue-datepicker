
<template>
  <transition name="slide-fade">
    <div v-if="show">
      <p>Select year</p>
      <!-- <button
        class="pointer"
        title="Scroll Up to choose previous years"
        @click="scrollToTop(-10)"
      >
        ▲
      </button> -->
      <div ref="wrapper" class="custom-tile scrollable">
        <div v-for="(y, index) in years" :key="index">
          <button @click="pickYear" class="custom-year-picker">
            {{ y }}
          </button>
        </div>
      </div>
      <!-- <button
        class="pointer"
        title="Scroll Up to choose previous years"
        @click="scrollToTop(+21)"
      >
        ▲
      </button> -->
    </div>
  </transition>
</template>


<script>
const DatePicker = {
  data() {
    return {
      show: false,
      currentYear: new Date().getFullYear(),
    };
  },

  computed: {
    years() {
      const year = new Date().getFullYear();
      const array = [];
      for (let i = year - 90; i < year; i++) array.push(i);
      return array;
    },
  },
  mounted() {
    this.show = true;
      this.$nextTick(function() {
       const container = this.$refs.wrapper;
      container.scrollTop = container.scrollHeight;
    });
   
  },

  methods: {
    pickYear(e) {
      this.show = false;
      this.$emit("yearPicked", e.target.textContent);
    },
    scrollToTop(value) {
      this.$refs.wrapper.scrollTop = value;
    },
  },
};
export default DatePicker;
</script>
<style scoped>
.custom-year-picker {
  background: none;
  cursor: pointer;
  padding: 8px;
  text-align: center;
  border-radius: 4px;
  margin: 0 auto;
  border: none;
}
.custom-year-picker:focus,
.custom-year-picker:active,
.custom-year-picker:hover {
  background: #ff7494;
  color: white;
}
.custom-tile {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-column-gap: 5px;
  grid-row-gap: 5px;
  max-width: 250px;
  min-height: 167px;
  max-height: 167px;
  margin: 25px auto;
}

.pointer {
  margin: 0 auto;
  cursor: pointer;
  border: none;
  background: none;
}

.scrollable {
  overflow: hidden;
  overflow-y: scroll;
  height: calc(100vh - 20px);
}
</style>
