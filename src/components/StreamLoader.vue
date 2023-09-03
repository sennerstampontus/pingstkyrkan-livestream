<template>
  <div class="container">
    <div class="loader"></div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
  name: 'StreamLoader',
  props: {
    loaderWidth: {
      type: String,
      default: '1/2',
    },
  },
});
</script>

<style lang="scss" scoped>
.loader {
  height: 10px;
  width: 45%;
  border-radius: 2px;
  background-color: rgba(0, 0, 0, 0.2);
  position: absolute;
}

.loader::before {
  content: '';
  position: absolute;
  background-color: rgb(202, 203, 201);
  width: 0%;
  height: 100%;
  border-radius: 2px;
  animation: load 5s ease-in-out infinite;
  box-shadow: rgb(180, 195, 154) 0px 2px 29px 0px;
}

.container {
  display: flex;
  justify-content: center;
}

@keyframes load {
  50% {
    width: 100%;
  }

  100% {
    right: 0;
    left: unset;
  }
}
</style>
