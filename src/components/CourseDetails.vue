<template>
  <div>
    {{details.description}}
    <p>{{details.prices[0].amount}}</p>
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
</template>
<script>
import moment from 'moment';

export default {
  name: 'CourseDetails',
  props: {
    details: { type: Object, required: true },
    location: { type: String },
  },
  computed: {
    formattedDates() {
      return this.details.start_dates.map((item) => moment(item).format('dddd, MMMM Do YYYY'));
    },
  },
};
</script>
<style>
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
