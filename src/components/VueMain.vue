<template>
  <main
    role="main"
    class="align-items-center container d-flex flex-column justify-content-center"
    style="height: calc(100vh - 10rem);"
  >
    <h2 class="pb-3">{{ $t("birth-text") }}</h2>

    <div class="input-group justify-content-center pb-3">
      <div class="input-group-prepend">
        <select class="input-group-text" v-model.number="day">
          <option v-for="i in days" :key="i">{{ i }}</option>
        </select>
      </div>
      <select class="select w-50" v-model.number="month">
        <option v-for="(month, mIndex) in months" :value="mIndex" :key="mIndex">{{ month }}</option>
      </select>
      <div class="input-group-append">
        <select class="input-group-text" v-model.number="year">
          <option v-for="(year, yIndex) in years" :key="yIndex">{{ year }}</option>
        </select>
      </div>
    </div>

    <div class="input-group justify-content-center align-items-center pb-3">
      <div class="input-group-prepend">
        <select class="input-group-text" v-model.number="hour">
          <option v-for="(hours, hIndex) in hours" :key="hIndex">{{ hours }}</option>
        </select>
      </div>
      <span class="px-1">:</span>
      <div class="input-group-append">
        <select class="input-group-text" v-model.number="minute">
          <option v-for="(minutes, mIndex) in minutes" :key="mIndex">{{ minutes }}</option>
        </select>
      </div>
    </div>

    <hr class="w-100 pb-3" />

    <div id="details">
      <p>{{ $t("yearsOld", { age: age, day: getDay }) }}</p>
      <p v-html="$t('haveBenn.months', { monthsPassed })"></p>
      <p v-html="$t('haveBenn.weeks', { weeksPassed })"></p>
      <p v-html="$t('haveBenn.days', { daysPassed })"></p>
      <p v-html="$t('haveBenn.hours', { hoursPassed })"></p>
      <p v-html="$t('haveBenn.minutes', { minutesPassed })"></p>
      <p v-html="$t('haveBenn.seconds', { secondsPassed })"></p>
    </div>

    <hr class="w-100 pb-3" />

    <div>
      <p>{{ `${$t("next", { nextBirthday })}` }}</p>
    </div>
    <h5 class="text-muted">Long live and prosper!</h5>
  </main>
</template>

<script>
export default {
  name: "VueMain",
  data() {
    return {
      year: 1900,
      years: [],
      month: 0,
      days: [],
      day: 1,
      hours: [],
      hour: 0,
      minute: 0,
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
    this.hours.unshift(0);
    this.minutes.unshift(0);
    this.month = date.getMonth() + 1;
    this.year = date.getFullYear();
    this.day = date.getDate();
    this.hour = 0;
    this.minute = 0;

    //test
    this.year = 1992;
    this.month = 8;
    this.day = 2;
    this.birthdate = new Date(
      this.year,
      this.month,
      this.day,
      this.hour,
      this.minute
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
      return this.weekDays[this.birthdate.getDate() % 7];
    },
    age() {
      return new Date().getFullYear() - this.year - 1;
    },
    diff() {
      return this.now - this.birthdate.getTime();
    },
    nextBirthday() {
      let date = new Date();
      let currentBirthday = new Date(
        date.getFullYear(),
        this.month,
        this.day,
        this.hour,
        this.minute
      );

      let diff = currentBirthday - date;
      if (currentBirthday < date) {
        diff = date - currentBirthday;
      }
      return Math.round(diff / (24 * 60 * 60 * 1000));
    },
    monthsPassed() {
      return this.format(this.age * 12 + (new Date().getMonth() + 1));
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
    }
  },
  watch: {
    year: function() {
      this.birthdate = new Date(
        this.year,
        this.month,
        this.day,
        this.hour,
        this.minute
      );
    },
    month: function() {
      this.birthdate = new Date(
        this.year,
        this.month,
        this.day,
        this.hour,
        this.minute
      );
    },
    day: function() {
      this.birthdate = new Date(
        this.year,
        this.month,
        this.day,
        this.hour,
        this.minute
      );
    },
    hour: function() {
      this.birthdate = new Date(
        this.year,
        this.month,
        this.day,
        this.hour,
        this.minute
      );
    },
    minute: function() {
      this.birthdate = new Date(
        this.year,
        this.month,
        this.day,
        this.hour,
        this.minute
      );
    }
  }
};
</script>

<style>
#details {
  font-size: 1.25rem;
}

p > span {
  font-weight: bold;
}
</style>
