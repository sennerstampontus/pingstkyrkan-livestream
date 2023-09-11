<template>
  <div class="grid h-screen w-100 place-items-center">
    <div class="grid w-1/3 grid-cols-2 gap-4 p-5 bg-gray-100 rounded-md h-1/2">
      <h1 class="col-span-2 pt-4 text-2xl text-center">Inställningar</h1>
      <div class="flex flex-col col-start-1">
        <label for="title"> Ange text </label>
        <input id="title" type="text" />
      </div>
      <div class="flex flex-col col-start-2">
        <label for="color"> Ange färg </label>
        <input id="color" type="text" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HomeView',
});
</script>
