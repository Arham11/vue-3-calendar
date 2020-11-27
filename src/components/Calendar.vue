<template>
  <h1 class="text-3xl mb-4 text-center">Calendar</h1>
  <div class="w-full sm:w-3/4 m-auto">
    <section class="flex justify-between">
      <h2 class="font-bold">{{ currentMonthName }}</h2>
      <h2 class="font-bold">{{ currentYear }}</h2>
    </section>
    <section style="height: 400px">
      <div class="flex day">
        <p
          class="w-1/7 p-3 text-center single-day"
          v-for="day in days"
          :key="day"
        >
          {{ day }}
        </p>
      </div>
      <div class="flex date flex-wrap">
        <p
          class="w-1/7 p-4 text-center single-date"
          v-for="space in startDay(currentYear, currentMonth)"
          :key="space"
        ></p>
        <p
          class="w-1/7 p-4 text-center single-date"
          v-for="date in dayInMonth(currentYear, currentMonth)"
          :key="date"
        >
          {{ date }}
        </p>
      </div>
    </section>
    <section class="flex justify-between">
      <button
        class="py-3 px-5 rounded-md bg-teal-500 text-white"
        @click="prevMonth"
      >
        prev
      </button>
      <button
        class="py-3 px-5 rounded-md bg-green-500 text-white"
        @click="nextMonth"
      >
        next
      </button>
    </section>
  </div>
</template>

<script lang="ts">
import { ref } from "vue";
export default {
  name: "calendar",
  setup() {
    //returns the name of the month in long letter format(alphabets)
    const currentMonthName = ref(
      new Date().toLocaleString("default", {
        month: "long"
      })
    );
    const currentMonth = ref(new Date().getMonth());
    const currentYear = ref(new Date().getFullYear());
    const days = ["Sun", "Mon", "Tues", "Wed", "Thurs", "Fri", "Sat"];
    const space = ref(0);

    //return number of days in month
    function dayInMonth(year, month) {
      return new Date(year, month + 1, 0).getDate(); // month array starts from 0 = January that is why added 1 for getDate()
    }

    //returns the starting space in month(if any)
    function startDay(year, month) {
      return (space.value = new Date(year, month, 1).getDay()); // month array starts from 1 = January for getDay()
    }

    //click to next month
    function nextMonth() {
      currentMonth.value++;
      currentMonthName.value = new Date(
        currentYear.value,
        currentMonth.value + 1,
        0
      ).toLocaleString("default", { month: "long" });
      if (currentMonth.value == 12) {
        currentYear.value++;
        currentMonth.value = 0;
      }
    }

    //click to previous month
    function prevMonth() {
      currentMonth.value--;
      currentMonthName.value = new Date(
        currentYear.value,
        currentMonth.value + 1,
        0
      ).toLocaleString("default", { month: "long" });
      if (currentMonth.value < 0) {
        currentYear.value--;
        currentMonth.value = 11;
      }
    }
    return {
      currentMonth,
      currentMonthName,
      currentYear,
      dayInMonth,
      days,
      space,

      startDay,
      nextMonth,
      prevMonth
    };
  }
};
</script>

<style lang="css" scoped>
.w-1\/7 {
  width: 14.285714285%;
}
</style>
