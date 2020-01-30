<template>
  <div id="app" class="font-sans min-h-screen bg-gray-300 flex flex-col justify-center items-center">
    <Metronome />
  </div>
</template>

<script>
import Metronome from './components/Metronome.vue'

export default {
  name: 'app',
  components: {
    Metronome
  }
}
</script>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
