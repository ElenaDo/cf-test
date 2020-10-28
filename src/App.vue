<template>
  <div id="app">
    <div class="row">
    <CourseCard
      v-for="course in courseList"
      :key="course.slug"
      :course="course"
      @select="selectCard(course.slug)"
      :active="selectedSlug === course.slug"
      :location="location"
    />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import CourseCard from './components/CourseCard.vue';

export default {
  name: 'App',
  components: {
    CourseCard,
  },
  data: () => ({
    courseList: [],
    selectedSlug: '',
    location: '',
  }),
  mounted() {
    this.getCourses();
    this.getLocation();
  },
  methods: {
    async get(path = '') {
      let result = {};
      try {
        const host = process.env.VUE_APP_HOST;
        result = await axios(host + path);
      } catch (err) {
        console.error(err);
      }
      return result.data;
    },
    async getCourses() {
      this.courseList = await this.get();
    },
    async getCourseDetails() {
      const index = this.courseList.findIndex((item) => item.slug === this.selectedSlug);
      if (!this.courseList[index].details) {
        const details = await this.get(`/${this.selectedSlug}`);
        // Vue.set to make new property reactive
        this.$set(this.courseList[index], 'details', details);
      }
    },
    async getLocation() {
      try {
        const key = process.env.VUE_APP_IPSTACK_KEY;
        const result = await axios(`http://api.ipstack.com/check?access_key=${key}`);
        if (result) this.location = result.data.continent_code;
      } catch (err) {
        console.error(err);
      }
    },
    selectCard(slug) {
      this.selectedSlug = slug;
      this.getCourseDetails();
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: TradeGothic,Helvetica,Arial,sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.row {
  display: flex;
  align-items: flex-start;
}
@media (max-width: 600px) {
  .row {
    flex-direction: column;
  }
}
</style>
