<template>
  <div class="music-player">
    <h2>Music Player</h2>
    <audio ref="audio" :src="currentTrack" controls></audio>
    <div class="controls">
      <button @click="play">Play</button>
      <button @click="pause">Pause</button>
      <button @click="stop">Stop</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currentTrack: {
      type: String,
      default: '',
    },
  },
  methods: {
    play() {
      this.$refs.audio.play();
    },
    pause() {
      this.$refs.audio.pause();
    },
    stop() {
      this.$refs.audio.pause();
      this.$refs.audio.currentTime = 0;
    },
  },
};
</script>

<style scoped>
.music-player {
  margin: 20px;
}
.controls button {
  margin: 5px;
}
</style>