<template>
  <livestream-starting></livestream-starting>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import LivestreamStarting from '@/components/LivestreamStarting.vue';
export default defineComponent({
  name: 'StreamView',
  components: {
    LivestreamStarting,
  },
});
</script>
