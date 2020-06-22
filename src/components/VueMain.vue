<template>
  <main
    role="main"
    class="align-items-center container d-flex flex-column justify-content-center"
    style="height: calc(100vh - 10rem);"
  >
    <h2 class="pb-3">{{ $t("birth-text") }}</h2>

    <div class="input-group justify-content-center pb-3">
      <div class="input-group-prepend">
        <select class="input-group-text" v-model.number="selectedDate.day">
          <option v-for="i in days" :key="i">{{ i }}</option>
        </select>
      </div>
      <select class="select w-50" v-model.number="selectedDate.month">
        <option v-for="(month, mIndex) in months" :value="mIndex" :key="mIndex">{{ month }}</option>
      </select>
      <div class="input-group-append">
        <select class="input-group-text" v-model.number="selectedDate.year">
          <option v-for="(year, yIndex) in years" :key="yIndex">{{ year }}</option>
        </select>
      </div>
    </div>

    <div class="input-group justify-content-center align-items-center">
      <div class="input-group-prepend">
        <select class="input-group-text" v-model.number="selectedDate.hour">
          <option v-for="(hours, hIndex) in hours" :key="hIndex">{{ hours }}</option>
        </select>
      </div>
      <span class="px-1">:</span>
      <div class="input-group-append">
        <select class="input-group-text" v-model.number="selectedDate.minute">
          <option v-for="(minutes, mIndex) in minutes" :key="mIndex">{{ minutes }}</option>
        </select>
      </div>
    </div>

    <div id="details" class="border border-info my-4 p-3 shadow">
      <p v-html="$t('yearsOld', { age: age, day: getDay })"></p>
      <p v-html="$t('haveBenn.months', { monthsPassed })"></p>
      <p v-html="$t('haveBenn.weeks', { weeksPassed })"></p>
      <p v-html="$t('haveBenn.days', { daysPassed })"></p>
      <p v-html="$t('haveBenn.hours', { hoursPassed })"></p>
      <p v-html="$t('haveBenn.minutes', { minutesPassed })"></p>
      <p v-html="$t('haveBenn.seconds', { secondsPassed })"></p>
    </div>

    <h4 v-html="$t('next', { nextBirthday }) + ' 💖'"></h4>

    <h5 class="text-muted mt-1">Long live and prosper!!</h5>
    <!-- <h5 class="text-muted">Yet in the darkness, there will be light..</h5> -->
  </main>
</template>

<script>
export default {
  name: "VueMain",
  data() {
    return {
      selectedDate: {
        year: 1900,
        month: 0,
        day: 1,
        minute: 0,
        hour: 0
      },
      years: [],
      days: [],
      hours: [],
      minutes: [],
      now: Date.now(),
      birthdate: null
    };
  },
  created() {
    let date = new Date();
    for (let i = 1; i < date.getFullYear() - 1898; i++) {
      if (i < 32) {
        this.days.push(i);
      }
      if (i < 24) {
        this.hours.push(i);
      }
      if (i < 60) {
        this.minutes.push(i);
      }
      this.years.push(i + 1899);
    }
    this.years.reverse();
    this.hours.unshift(0);
    this.minutes.unshift(0);

    // test with my own birthday :)
    this.selectedDate.day = 2;
    this.selectedDate.month = 8;
    this.selectedDate.year = 1992;

    this.birthdate = new Date(
      this.selectedDate.year,
      this.selectedDate.month,
      this.selectedDate.day,
      this.selectedDate.hour,
      this.selectedDate.minute
    );

    this.now = Date.now();
    setInterval(() => (this.now = Date.now()), 1000);
  },
  methods: {
    format(value, indicator = ".") {
      return value.toString().replace(/(.)(?=(?:\d{3})+$)/g, "$1" + indicator);
    }
  },
  computed: {
    months() {
      return this.$t("months");
    },
    weekDays() {
      return this.$t("weekDays");
    },
    getDay() {
      return this.weekDays[this.birthdate.getDay()];
    },
    age() {
      return new Date().getFullYear() - this.selectedDate.year;
    },

    diff() {
      return this.now - this.birthdate.getTime();
    },
    monthsPassed() {
      let MONTH = 1000 * 60 * 60 * 24 * 30;
      let currentMonth = new Date().getMonth();
      let _month = Math.floor(this.diff / MONTH) - currentMonth;
      if (currentMonth > this.selectedDate.month) {
        _month--;
      }
      return this.format(_month);
    },
    weeksPassed() {
      return this.format(Math.floor(this.diff / (1000 * 60 * 60 * 24 * 7)));
    },
    daysPassed() {
      return this.format(Math.floor(this.diff / (1000 * 60 * 60 * 24)));
    },
    hoursPassed() {
      return this.format(Math.floor(this.diff / (1000 * 60 * 60)));
    },
    minutesPassed() {
      return this.format(Math.floor(this.diff / (1000 * 60)));
    },
    secondsPassed() {
      return this.format(Math.floor(this.diff / 1000));
    },
    nextBirthday() {
      let date = new Date();
      let nextBirthDay = new Date(
        date.getFullYear(),
        this.selectedDate.month,
        this.selectedDate.day
      );
      let next = Math.round((nextBirthDay - date) / (24 * 60 * 60 * 1000));
      if (next < 0) {
        next = 365 - Math.abs(next);
      }
      return next;
    }
  },
  watch: {
    selectedDate: {
      handler: function() {
        this.birthdate = new Date(
          this.selectedDate.year,
          this.selectedDate.month,
          this.selectedDate.day,
          this.selectedDate.hour,
          this.selectedDate.minute
        );
      },
      deep: true
    }
  }
};
</script>

<style>
#details {
  font-size: 1.25rem;
  border-radius: 1.5rem;
}

p {
  margin-bottom: 0.5rem;
}

p > span {
  font-weight: bold;
}
</style>
