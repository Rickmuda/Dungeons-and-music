<template>
  <div id="app">
    <header>
      <h1>Dungeon Music Player</h1>
    </header>
    <main>
      <!-- Left Side: Song Selector -->
      <div class="left-panel">
        <h3>Scenes</h3>
        <div class="image-grid">
          <button
            v-for="(scene, index) in scenes"
            :key="index"
            @click="switchSong(scene.youtubeId)"
          >
            <img :src="scene.image" :alt="scene.name" />
            <p>{{ scene.name }}</p>
          </button>
        </div>
      </div>

      <!-- Right Side: Sound Effects -->
      <div class="right-panel">
        <h3>Sound Effects</h3>
        <div class="image-grid">
          <button
            v-for="(effect, index) in soundEffects"
            :key="index"
            @click="playSoundEffect(effect.youtubeId)"
          >
            <img :src="effect.image" :alt="effect.name" />
            <p>{{ effect.name }}</p>
          </button>
        </div>
      </div>
    </main>

    <!-- Footer: YouTube Players -->
    <footer class="audio-controls">
      <h3>Audio Controls</h3>
      <div class="youtube-players">
        <iframe
          v-if="currentSongYouTubeId"
          :src="`https://www.youtube.com/embed/${currentSongYouTubeId}?autoplay=1`"
          frameborder="0"
          allow="autoplay; encrypted-media"
          allowfullscreen
        ></iframe>
        <iframe
          v-if="currentEffectYouTubeId"
          :src="`https://www.youtube.com/embed/${currentEffectYouTubeId}?autoplay=1`"
          frameborder="0"
          allow="autoplay; encrypted-media"
          allowfullscreen
        ></iframe>
      </div>
    </footer>
  </div>
</template>

<script>
import './App.css'; // Import the CSS file

export default {
  data() {
    return {
      currentSongYouTubeId: null, // Holds the currently playing YouTube video ID for songs
      currentEffectYouTubeId: null, // Holds the currently playing YouTube video ID for sound effects
      scenes: [
        { name: 'Tavern', image: require('@/assets/img/scenes/tavern.png'), youtubeId: 'vyg5jJrZ42s' },
        { name: 'Battle', image: require('@/assets/img/scenes/battle.png'), youtubeId: 'sd1Otp7s1Fk' },
        { name: 'Forest', image: require('@/assets/img/scenes/forest.png'), youtubeId: '6Em9tLXbhfo' },
        { name: 'Dungeon', image: require('@/assets/img/scenes/dungeon.png'), youtubeId: 'bxoRRobHtGM' },
        { name: 'Castle', image: require('@/assets/img/scenes/castle.png'), youtubeId: 'BwV1azM1Ifw' },
        { name: 'Village', image: require('@/assets/img/scenes/village.png'), youtubeId: 'jyYnGLh5vL0' },
        { name: 'Cave', image: require('@/assets/img/scenes/cave.png'), youtubeId: '3Hwr_BaekgM' },
        { name: 'Ship', image: require('@/assets/img/scenes/ship.png'), youtubeId: 'beOw8MEojQ4' },
      ],
      soundEffects: [
        { name: 'Cheer', image: require('@/assets/img/sfx/cheer.png'), youtubeId: 'idA7RsiOpqA' },
        { name: 'Sword Clash', image: require('@/assets/img/sfx/sword-clash.png'), youtubeId: 'E8Ced6hW45k' },
        { name: 'Birdsong', image: require('@/assets/img/sfx/birdsong.png'), youtubeId: 'hhz6AI45IQw' },
        { name: 'Chains', image: require('@/assets/img/sfx/chains.png'), youtubeId: 'Z_FsyK92Zjc' },
        { name: 'Trumpet', image: require('@/assets/img/sfx/trumpet.png'), youtubeId: 'a6_R6x5pbpg' },
        { name: 'Footsteps', image: require('@/assets/img/sfx/footsteps.png'), youtubeId: 'mPgGg4MJKKc' },
      ],
    };
  },
  methods: {
    switchSong(youtubeId) {
      this.currentSongYouTubeId = youtubeId; // Set the current YouTube video ID for songs
    },
    playSoundEffect(youtubeId) {
      this.currentEffectYouTubeId = youtubeId; // Set the current YouTube video ID for sound effects
    },
  },
};
</script>

<style>
/* Add your styles here */
.audio-controls .youtube-players iframe {
  width: 100%;
  height: 150px;
  margin-bottom: 10px;
}
</style>
