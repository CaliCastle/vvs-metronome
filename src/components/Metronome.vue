<template>
  <div class="metronome flex flex-col items-center">
    <img src="@/assets/logo.png" alt="Logo" class="w-32 h-32" id="vvs-logo" />
    <h1 class="text-2xl font-bold font-mono text-gray-700">VVS Metronome</h1>

    <section class="flex flex-col items-center w-full mt-6">
      <input type="range" min="60" max="220" v-model="bpm" class="w-64 my-6" @input="onBPMChange" />
      <span class="font-mono mb-4 flex items-center">
        <span class="mr-2 text-xl">BPM:</span>
        <span class="text-6xl">{{ bpm }}</span>
      </span>
      <button
        class="w-24 text-white rounded-lg shadow-lg outline-none focus:outline-none py-2 font-medium"
        :class="[playing ? 'bg-red-500' : 'bg-blue-500']"
        @click.prevent="playOrStop"
        v-text="playing ? 'Stop' : 'Play'"
      />
    </section>
  </div>
</template>

<script>
import click_a from '@/assets/click_a.wav'
import click_b from '@/assets/click_b.wav'

export default {
  data() {
    return {
      bpm: 100,
      playing: false,
      sounds: [],
      step: 0,
      timer: 0
    };
  },

  created() {
    this.sounds = [new Audio(click_a), new Audio(click_b)]

    for (const sound of this.sounds) {
      sound.volume = 0.6
    }
  },

  methods: {
    playOrStop() {
      if (this.playing) {
        clearInterval(this.timer)
      } else {
        this.timer = setInterval(this.playSound, (60 / this.bpm) * 1000)
        this.playSound()
      }
      this.playing = !this.playing
    },
    playSound() {
      this.step++
      this.sounds[this.step % 2].play()
    },
    onBPMChange() {
      if (this.playing) {
        clearInterval(this.timer)
        this.timer = setInterval(this.playSound, (60 / this.bpm) * 1000)
      }
    }
  }
};
</script>

<style>
#vvs-logo {
  filter: invert(0.6);
}
</style>
