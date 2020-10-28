<template>
  <div id="app">
    <div v-for="course in coursesList" :key="course.slug">
      {{course.title}}
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  components: {
  },
  data: () => ({
    coursesList: [],
  }),
  mounted() {
    this.getCourses();
  },
  methods: {
    async getCourses() {
      try {
        const host = process.env.VUE_APP_HOST;
        const result = await axios(host);
        this.coursesList = result.data;
        console.log(this.coursesList);
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
</style>
