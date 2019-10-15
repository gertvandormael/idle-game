<template>
  <div class="game">
    <div class="header">
      <h1>Bandcremental</h1>
      <p>Become the greatest band ever!</p>
    </div>
    <div class="clicker">
      <div class="skill">
        <img
          src="../assets/band.jpg"
          alt="band image"
        >
        Skill: {{ incremental.skill }}
        <button @click="increaseSkill">Practice</button>
      </div>
      <div class="info">
        <h2>Info</h2>
        Click power: {{ incremental.skillPerClick }} <br>
        Idle gain: {{ incremental.idleSkillGain }}
      </div>
    </div>

    <div class="upgrades">
      <h2>Songs</h2>
      <div class="song">
        <h3>Smoke on the water - Deep Purple</h3>
        <p>Gain 1 click power and 0.5 idle power</p>
        <button
          @click="learnFirstSong"
          :disabled="skillCheckFirstSong"
          v-if="!upgrades.disableFirstSong"
        >Learn song</button>
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
  data() {
    return {
      incremental: {
        skill: 0,
        skillPerClick: 1,
        idleSkillGain: 0,
      },
      upgrades: {
        purchasedFirstsong: false,
        disableFirstSong: false
      }
    };
  },

  computed: {
    skillCheckFirstSong() {
      if (this.incremental.skill < 10) {
        return true;
      } else if (this.incremental.skill >= 10) {
        return false;
      }
    },
  },

  methods: {
    increaseSkill() {
      this.incremental.skill += this.incremental.skillPerClick;
    },

    learnFirstSong() {
      this.incremental.skillPerClick += 1;
      this.incremental.idleSkillGain += 0.5;
      this.upgrades.disableFirstSong = true;
    },

    idleGains() {
      setInterval(() => {this.incremental.skill += this.incremental.idleSkillGain}, 1000);
    },
  },

  mounted() {
    this.idleGains();
  }


};
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  img {
    max-width: 250px;
    max-width: 250px;
  }
  .header {
    margin-bottom: 15px;
  }

  body {
    margin-left: 15px;
  }

  h2 {
    margin-top: 10px;
  }
</style>