<template>
  <div class="game">
    <div class="header">
      <h1>Bandcremental</h1>
      <p>Become the greatest band ever!</p>
    </div>
    <div class="clicker">
      <div class="band">
        <img
          src="../assets/band.png"
          alt="band image"
          @click="increaseSkill"
          :class="{ applyShake: isActive }"
        >
      </div>
      <div class="skill">
       <h3>Skill: {{ incremental.skill }}</h3> 
      </div>
    </div>
    <div class="info">
      <h2>Info</h2>
      Click power: {{ incremental.skillPerClick }} <br>
      Idle gain: {{ incremental.idleSkillGain }}
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
        >Learn
          song</button>
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
        idleSkillGain: 0
      },
      upgrades: {
        purchasedFirstsong: false,
        disableFirstSong: false
      },
      isActive: false,
    };
  },

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
    increaseSkill() {
      this.incremental.skill += this.incremental.skillPerClick;
      this.isActive = !this.isActive;
    },

    learnFirstSong() {
      this.incremental.skillPerClick += 1;
      this.incremental.idleSkillGain += 0.5;
      this.upgrades.disableFirstSong = true;
    },

    idleGains() {
      setInterval(() => {
        this.incremental.skill += this.incremental.idleSkillGain;
      }, 1000);
    }
  },

  mounted() {
    this.idleGains();
  }
};
</script>

<style>
/* Game specific layout */
  .header {
    margin-bottom: 15px;
  }

  /* .band {
    display: flex;
    justify-content: center;
  } */

  .header p {
    color: #ff6fd2;
  }

  img {
    max-width: 250px;
    max-width: 250px;
  }

  body {
    background: #824438;
  }

  button {
    font-family: 'Press Start 2P', cursive;
    background: #ff6fd2;
    border: none;
    width: 100px;
  }

  button:disabled {
    background: white
  }

  button:active:hover {
    background: #cbdbfc;
    color: #ff6fd2;
  }

@keyframes shake {
  10%, 90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%, 80% {
    transform: translate3d(2px, 0, 0);
  }

  30%, 50%, 70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%, 60% {
    transform: translate3d(4px, 0, 0);
  }
}

.applyShake {
    animation: shake 0.82s cubic-bezier(.36,.07,.19,.97) both;
}



</style>