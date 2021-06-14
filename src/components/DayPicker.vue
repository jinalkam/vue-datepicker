
<template>
  <div>
    <p>Select a day</p>
    <div class="custom-day">
      <div v-for="d in 31" :key="d">
        <button
          :style="currentDate == d ? 'border: 1px solid black' : 'none'"
          @click="pickDate"
        >
          {{ d }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      days: [],
      currentDate: new Date().getDate(),
    };
  },
  methods: {
    pickDate(e) {
      this.$emit("datePicked", e.target.textContent);
    },
  },
};
</script>
<style scoped>
button {
  background: none;
  cursor: pointer;
  padding: 4px;
  text-align: center;
  width: 32px;
  border-radius: 4px;
  border: none;
  height: 32px;
  margin: 0 auto;
}
button:focus,
button:active,
button:hover {
  background: #ff7494;
  color: white;
}
.custom-day {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-column-gap: 5px;
  grid-row-gap: 5px;
  max-width: 250px;
  max-height: 217px;
  margin: 0 auto;
}

</style>