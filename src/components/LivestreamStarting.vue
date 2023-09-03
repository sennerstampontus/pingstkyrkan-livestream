<template>
  <!-- Add your code here -->
</template>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
  name: 'LivestreamStarting',

  computed: {
    getQuery() {
      return this.$route.query;
    },
  },
  mounted() {
    console.log(this.getQuery);
  },
});
</script>
