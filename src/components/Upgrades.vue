<template>
  <div class="upgrades">
    <h2>Songs</h2>
    <div class="song">
      <h3>Smoke on the water - Deep Purple</h3>
      <p>Gain 1 click power and 0.5 idle power</p>
      <div class="first-song">
        <button
          @click="learnFirstSong"
          :disabled="skillCheckFirstSong"
          v-if="!upgrades.disableFirstSong"
        > Learn song!
        </button>
        <div
          class="require"
          v-if="!upgrades.disableFirstSong"
        >Requires 10 skill</div>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  computed: {
    skillCheckFirstSong() {
      if (this.incremental.skill < 10) {
        return true;
      } else if (this.incremental.skill >= 10) {
        return false;
      }
    }
  },

  methods: {
    learnFirstSong() {
      this.incremental.skillPerClick += 1;
      this.incremental.idleSkillGain += 0.5;
      this.upgrades.disableFirstSong = true;
    }
  }
};
</script>

<style>

</style>