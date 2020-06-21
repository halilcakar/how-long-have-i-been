<template>
  <div>
    <h2>{{ $t("title") }}</h2>

    <div>
      <h4>
        {{ $t("birth-text") }}
      </h4>

      <div class="birthdate">
        <select v-model.number="day">
          <option v-for="i in days" :key="i">{{ i }}</option>
        </select>
        <select v-model.number="month">
          <option v-for="(m, mIndex) in months" :value="mIndex" :key="mIndex">{{
            m
          }}</option>
        </select>
        <select v-model.number="year">
          <option v-for="(y, yIndex) in years" :key="yIndex">{{ y }}</option>
        </select>
      </div>

      <div id="hour-details" class="birthdate">
        <select v-model.number="hour">
          <option v-for="(h, hIndex) in hours" :key="hIndex">{{ h }}</option>
        </select>
        <select v-model.number="minute">
          <option v-for="(m, mIndex) in minutes" :key="mIndex">{{ m }}</option>
        </select>
      </div>

      <hr />

      <div id="details">
        <p>{{ $t("yearsOld", { age, day: getDay }) }}</p>
        <p v-html="$t('haveBenn.months', { monthsPassed })"></p>
        <p v-html="$t('haveBenn.weeks', { weeksPassed })"></p>
        <p v-html="$t('haveBenn.days', { daysPassed })"></p>
        <p v-html="$t('haveBenn.hours', { hoursPassed })"></p>
        <p v-html="$t('haveBenn.minutes', { minutesPassed })"></p>
        <p v-html="$t('haveBenn.seconds', { secondsPassed })"></p>
        <p>{{ $t("haveBenn.passed") }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      year: "",
      years: [],
      month: 0,
      days: [],
      day: 1,
      hours: [],
      hour: 0,
      minute: 0,
      minutes: [],
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
    this.year = 1992;
    this.month = 8;
    this.day = 2;
  },
  methods: {
    format(value, indicator = ".") {
      return value.toString().replace(/(.)(?=(?:\d{3})+$)/g, "$1" + indicator);
    },
  },
  computed: {
    months() {
      return this.$t("months");
    },
    weekDays() {
      return this.$t("weekDays");
    },
    getDay() {
      return this.weekDays[this.birthdate.getDay() - 1];
    },
    birthdate() {
      return new Date(this.year, this.month, this.day, this.hour, this.minute);
    },
    diff() {
      return new Date(Date.now() - this.birthdate.getTime()).getTime();
    },
    age() {
      return new Date().getFullYear() - this.year - 1;
    },
    monthsPassed() {
      return this.format(Math.floor(this.diff / (1000 * 60 * 60 * 24 * 30)));
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
  },
};
</script>

<style>
.birthdate {
  display: flex;
  justify-content: center;
}
#hour-details {
  margin-top: 1rem;
}

#details {
  font-size: 1.5rem;
}

span {
  font-weight: bold;
}

select {
  padding: 0.5%;
  border-radius: 10%;
  border-color: grey;
}
select:nth-child(2) {
  margin: 0 2.5% 0 2.5%;
}

hr {
  margin: 1rem 0;
  border-width: 0.5px;
  color: #d3d3d3;
}
</style>
