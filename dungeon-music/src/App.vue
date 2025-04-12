<template>
  <div id="app">
    <header class="header-grid">
        <!-- Left Block: YouTube Video for Scenes -->
        <div class="youtube-player" ref="songPlayerContainer"></div>

        <!-- Middle Block: Title -->
        <h1>Dungeons And Music</h1>

        <!-- Right Block: YouTube Video for Sound Effects -->
        <div class="youtube-player" ref="effectPlayerContainer"></div>

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
  </div>
</template>

<script>
import './App.css'; // Import the CSS file

export default {
  data() {
    return {
      songPlayer: null, // YouTube player for songs
      effectPlayer: null, // YouTube player for sound effects
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
    loadYouTubeAPI() {
      if (!window.YT) {
        const tag = document.createElement('script');
        tag.src = 'https://www.youtube.com/iframe_api';
        const firstScriptTag = document.getElementsByTagName('script')[0];
        firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
      } else {
        this.onYouTubeIframeAPIReady();
      }
    },
    onYouTubeIframeAPIReady() {
      this.songPlayer = new window.YT.Player(this.$refs.songPlayerContainer, {
        height: '100',
        width: '300',
        events: {
          onReady: (event) => {
            event.target.setVolume(20); // Set volume to 20%
          },
        },
      });

      this.effectPlayer = new window.YT.Player(this.$refs.effectPlayerContainer, {
        height: '100',
        width: '300',
        events: {
          onReady: (event) => {
            event.target.setVolume(20); // Set volume to 20%
          },
        },
      });
    },
    switchSong(youtubeId) {
      if (this.songPlayer) {
        this.songPlayer.loadVideoById(youtubeId);
      }
    },
    playSoundEffect(youtubeId) {
      if (this.effectPlayer) {
        this.effectPlayer.loadVideoById(youtubeId);
      }
    },
  },
  mounted() {
    this.loadYouTubeAPI();
    window.onYouTubeIframeAPIReady = this.onYouTubeIframeAPIReady;
  },
};
</script>
