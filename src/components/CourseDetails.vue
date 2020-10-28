<template>
  <div class="details-container">
    <div v-if="details">
      {{details.description}}
      <p>Price: {{price.symbol}}{{price.amount}}</p>
      <div class="next-start-dates">
        <p>Next start dates:</p>
        <ul>
          <li
            v-for="(item,i) in formattedDates.slice(1)"
            :key="i" class="dates-list-items"
          >
            {{item}}
          </li>
        </ul>
      </div>
    </div>
    <Loading v-else />
  </div>
</template>
<script>
import moment from 'moment';
import Loading from './Loading.vue';

export default {
  name: 'CourseDetails',
  components: { Loading },
  props: {
    details: { type: Object },
    location: { type: String },
  },
  computed: {
    formattedDates() {
      return this.details.start_dates.map((item) => moment(item).format('dddd, MMMM Do YYYY'));
    },
    price() {
      const currency = this.location === 'EU' ? 'eur' : 'usd';
      const { amount } = this.details.prices.find((item) => item.currency === currency);
      const symbol = this.location === 'EU' ? '€' : '$';
      return { amount, symbol };
    },
  },
};
</script>
<style>
div.details-container {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.5s;
}
.active div.details-container{
  max-height: 250px;
}
.next-start-dates p {
  font-size: 0.9em;
  margin-bottom: 0px;
}
.next-start-dates ul {
  list-style-type: none;
  padding: 0;
  margin-top: 0.2em;
}
.next-start-dates li {
  color: #a7b1b9;
  font-size: 0.9em;
  margin: 0.1em;
}
</style>
