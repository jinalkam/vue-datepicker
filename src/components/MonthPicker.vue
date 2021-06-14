
<template>
  <transition name="slide-fade">
    <div v-if="show">
    <p>Select month</p>
    <div class="custom-tile">
       <div v-for="(m, index) in months" :key="index">
        <button
          :data-month="index + 1"
          @click="pickMonth"
        >
          {{ m }}
        </button>
      </div>


    </div>
    </div>
  </transition>
</template>
<script>

export default {
  data() {
    return {
      show: false,
      months: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ],
      monthWith30days: ["February", "April", "June", "September", "November"],
      today: new Date(),
    };
  },
  props: ["date"],
  mounted() {
      this.show = true;
 
  },

  methods: {
    pickMonth(e) {
      this.$emit("monthPicked", e.target.dataset.month);
    },
  },
};

</script>

<style scoped>
button {
  background: none;
  cursor: pointer;
  padding: 8px;
  text-align: center;
  border-radius: 4px;
  margin: 0 auto;
  border: none;
}
button:focus,
button:active,
button:hover {
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


</style>
