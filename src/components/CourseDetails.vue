<template>
  <div>
    {{details.description}}
    <p>{{details.prices[0].amount}}</p>
  </div>
</template>
<script>
export default {
  name: 'CourseDetails',
  props: {
    details: { type: Object, required: true },
  },
};
</script>
<style>

</style>
