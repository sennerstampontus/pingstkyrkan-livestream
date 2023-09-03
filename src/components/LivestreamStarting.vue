<template>
  <div class="grid h-screen text-3xl place-items-center">
    <div>
      <div class="flex gap-5">
        <template v-if="!isTimeExpired">
          <h1 class="mb-5" :style="`color:${getTextColorQuery}`">
            {{ getTextQuery }}
          </h1>
          <p v-if="getTimeQuery" :style="`color:${getTimeColorQuery}`">
            <b>{{ countdown }}</b>
          </p>
        </template>
        <template v-else>
          <h1 class="mb-5" :style="`color:${getTextColorQuery}`">
            Sändningen börjar strax
          </h1>
        </template>
      </div>

      <stream-loader :loader-width="getLoaderWidthQuery"></stream-loader>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import StreamLoader from './StreamLoader.vue';
export default defineComponent({
  name: 'LivestreamStarting',
  components: {
    StreamLoader,
  },
  data() {
    return {
      countdown: '',
      setCountdownFalse: false,
    };
  },

  computed: {
    getTextQuery() {
      return this.$route.query['streaming-text'];
    },
    getTimeQuery() {
      return this.$route.query['countdown-to'] as string;
    },
    getTextColorQuery() {
      return this.$route.query['text-color'] as string;
    },
    getTimeColorQuery() {
      return this.$route.query['time-color'] as string;
    },
    getLoaderWidthQuery() {
      return this.$route.query['loader-width'] as string;
    },
    isTimeExpired() {
      const queryTime = this.convertTime();
      const target = new Date();
      target.setHours(queryTime.hour);
      target.setMinutes(queryTime.minute);
      target.setSeconds(0);
      target.setMilliseconds(0);

      return target.getTime() < Date.now();
    },
  },
  mounted() {
    this.startCountdown();
  },

  watch: {
    getTimeQuery: function () {
      this.startCountdown();
    },
  },
  methods: {
    // Countdown minutes and seconds to the specified hour of the day
    // Time can be in format 0-23 (24 hour clock) with hours only or hours and minutes
    startCountdown() {
      if (!this.setCountdownFalse) {
        const time = this.convertTime();

        const now = new Date();
        const target = new Date();
        if (typeof time === 'number') {
          target.setHours(time);
          target.setMinutes(0);
          target.setSeconds(0);
          target.setMilliseconds(0);
        } else {
          target.setHours(time.hour);
          target.setMinutes(time.minute);
          target.setSeconds(0);
          target.setMilliseconds(0);
        }

        const diff = target.getTime() - now.getTime();
        const minutes = Math.floor(diff / 1000 / 60);
        const seconds = Math.floor(diff / 1000) - minutes * 60;
        const countdown = `${minutes}:${seconds.toString().padStart(2, '0')}`;
        this.countdown = countdown;

        if (countdown === '0:00') {
          window.location.reload();
          this.setCountdownFalse = true;
        } else setTimeout(this.startCountdown, 1000);
      } else return;
    },
    // If get time query is in format 23:05, convert so that it can be used in the countdown function
    convertTime() {
      if (this.getTimeQuery?.includes(':')) {
        const [hour, minute] = this.getTimeQuery.split(':').map(Number);

        return { hour, minute };
      } else return { hour: Number(this.getTimeQuery), minute: 0 };
    },
  },
});
</script>
