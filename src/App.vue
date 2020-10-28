<template>
  <div id="app">
    <div class="row">
    <CourseCard
      v-for="course in courseList"
      :key="course.slug"
      :course="course"
      @select="selectCard(course.slug)"
      :active="selectedSlug === course.slug"
      :courseDetails = "courseDetails"
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
    courseDetails: {},
    selectedSlug: '',
  }),
  mounted() {
    this.getCourses();
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
      this.courseDetails = await this.get(`/${this.selectedSlug}`);
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
  font-family: Avenir, Helvetica, Arial, sans-serif;
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
</style>
