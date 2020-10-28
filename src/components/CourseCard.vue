<template>
  <div class="course-card">
    {{course.title}}
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

<style lang="scss" scoped>
.course-card {
  background-color: #f0f1f3;
}
</style>
