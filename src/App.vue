<template>
  <div id="app">
    <div class="row">
    <CourseCard
      v-for="course in courseList"
      :key="course.slug"
      :course="course"
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
  }),
  mounted() {
    this.getCourses();
  },
  methods: {
    async getCourses() {
      try {
        const host = process.env.VUE_APP_HOST;
        const result = await axios(host);
        this.courseList = result.data;
      } catch (err) {
        console.error(err);
      }
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
}
</style>
