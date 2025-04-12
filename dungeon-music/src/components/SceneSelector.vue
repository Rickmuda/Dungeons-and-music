<template>
  <div class="scene-selector">
    <h2>Select a Scene</h2>
    <select v-model="selectedScene" @change="onSceneChange">
      <option v-for="scene in scenes" :key="scene" :value="scene">
        {{ scene }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedScene: '',
      scenes: ['Tavern', 'Battle', 'Forest', 'Dungeon', 'Castle'],
    };
  },
  methods: {
    onSceneChange() {
      this.$emit('scene-changed', this.selectedScene);
    },
  },
};
</script>

<style scoped>
.scene-selector {
  margin: 20px;
}
</style>