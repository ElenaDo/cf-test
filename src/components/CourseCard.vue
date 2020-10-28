<template>
  <div :class="[{'active': active}, 'course-card']">
    <div class="card-body">
    <h3>{{course.title}}</h3>
    <p>Course starts on {{course.next_start_formatted}}</p>
    </div>
    <CourseDetails v-if="active && course.details" :details="course.details"/>
    <button v-if="!active" class="course-card-button" @click="select">
      See details
    </button>
  </div>
</template>
<script>
import CourseDetails from './CourseDetails.vue';

export default {
  name: 'CourseCard',
  components: {
    CourseDetails,
  },
  props: {
    course: Object,
    active: Boolean,
    courseDetails: Object,
  },
  methods: {
    select() {
      this.$emit('select');
    },
  },
};
</script>

<style scoped>
.course-card {
  background-color: #f0f1f3;
  border: 1px solid #2c3e50;
  border-radius: 5px;
  width: 300px;
  margin: 2em;
  padding: 1em;
}
.active.course-card {
  background-color: #fff;
}
.card-body {
  min-height: 8em;
}
.course-card-button {
  background-color: #5ca2b2;
  border: 0;
  cursor: pointer;
  margin: auto;
  color: #fff;
  border-radius: 5px;
  padding: 0.5em 1em;
}
.course-card-button:focus {
  outline: none;
}
</style>
