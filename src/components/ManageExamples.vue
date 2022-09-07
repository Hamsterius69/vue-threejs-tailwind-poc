<template>
  <div class="grid grid-cols-2 gap-4">
    <div>
        <example-1 />
    </div>
    <div>
        <example-2 />
    </div>
  </div>
</template>

<script>
import Example1 from './Example1.vue';
import Example2 from './Example2.vue';

export default {
  name: 'ManageExamples',
  components: {
    Example1,
    Example2,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>