<template>
  <div class="course-card">
    <div class="card-body">
    <h3>{{course.title}}</h3>
    </div>
  <button class="course-card-button">
    See details
  </button>
  </div>
</template>
<script>
export default {
  name: 'CourseCard',
  props: {
    course: Object,
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
