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
        >
      </div>
      <div class="data">
        <div class="skill">
          <h3>Skill {{ incremental.skill }}</h3>
          <h3>Cash </h3>
          <h3>Fame </h3>
        </div>
        <div class="info">
          <h2>Info</h2>
          <p>Click power: {{ incremental.skillPerClick }}</p>
          <p>Idle gain: {{ incremental.idleSkillGain }}</p>
        </div>
      </div>
    </div>

    <div class="upgrades">
      <div class="song-upgrades">
        <h2>Songs</h2>
        <div class="song">
          <div class="song-info">
            <div class="song-pic">
              <img
                v-if="!songUpgrades.disableSong[0]"
                src="../assets/song-locked.png"
                alt="song locked"
              >
              <img
                v-if="songUpgrades.disableSong[0]"
                src="../assets/song-unlocked.png"
                alt="song unlocked"
              >
            </div>
            <h3 :class="{ songLocked: !songUpgrades.disableSong[0] }">
              Smoke On The Water - Deep Purple
            </h3>
          </div>
          <div class="song-button">
            <button
              @click="learnSong(0)"
              :disabled="skillCheckFirstSong"
              v-if="!songUpgrades.disableSong[0]"
            > Learn song!
            </button>
            <div
              class="requirements"
              v-if="!songUpgrades.disableSong[0]"
            >
              <p>Requires 10 skill</p>
              <p>Gain 1 click power and 0.5 idle power</p>
            </div>

          </div>
        </div>
        <div class="song">
          <div class="song-info">
            <div class="song-pic">
              <img
                v-if="!songUpgrades.disableSong[1]"
                src="../assets/song-locked.png"
                alt="song locked"
              >
              <img
                v-if="songUpgrades.disableSong[1]"
                src="../assets/song-unlocked.png"
                alt="song unlocked"
              >
            </div>
            <h3 :class="{ songLocked: !songUpgrades.disableSong[1] }">
              Highway to Hell - AC/DC
            </h3>
          </div>
          <div class="song-button">
            <button
              @click="learnSong(1)"
              :disabled="skillCheckSecondSong"
              v-if="!songUpgrades.disableSong[1]"
            >
              Learn song!
            </button>
            <div
              class="requirements"
              v-if="!songUpgrades.disableSong[1]"
            >
              <p>Requires 50 skill</p>
              <p>Gain 5 click power and 2 idle power </p>
            </div>
          </div>

        </div>

      </div>

      <div class="gear-upgrades">
        <h2>Gear</h2>
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
        cash: 0,
        fame: 0
      },
      songUpgrades: {
        skill: [1, 2],
        idle: [1, 2],
        disableSong: [false, false],
        disableFirstSong: false,
        disableSecondSong: false
      }
    };
  },

  computed: {
    skillCheckFirstSong() {
      if (this.incremental.skill < 10) {
        return true;
      } else {
        return false;
      }
    },

    skillCheckSecondSong() {
      if (this.incremental.skill < 50) {
        return true;
      } else {
        return false;
      }
    }
  },

  methods: {
    increaseSkill() {
      this.incremental.skill += this.incremental.skillPerClick;
    },

    learnFirstSong() {
      this.incremental.skillPerClick += 1;
      this.incremental.idleSkillGain += 1;
      this.songUpgrades.disableFirstSong = true;
    },

    learnSong(number) {
      this.incremental.skillPerClick += this.songUpgrades.skill[number];
      this.incremental.idleSkillGain += this.songUpgrades.idle[number];
      this.songUpgrades.disableSong[number] = true;
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
  /* .upgrades {
    display: flex;
  } */

  .band {
    display: flex;
    justify-content: center;
  }

  img {
    max-width: 250px;
    max-width: 250px;
  }

  button {
    font-family: 'Press Start 2P', cursive;
    background: #ff6fd2;
    color: #cbdbfc;
    border: none;
    width: 100px;
    height: 50px;
    margin-right: 10px;
  }

  button:disabled {
    background: #969696
  }

  button:hover:enabled {
    background: #cbdbfc;
    color: #ff6fd2;
  }

  .song-info, .song-button {
    display: flex;
  }

  .song-info h3 {
    align-self: center;
  }
  
  .requirements {
    align-self: center;
  }

  .songLocked {
    color: #dadada;
    text-shadow:
      -2px -2px 0 #000000,
      2px -2px 0 #000000,
      -2px 2px 0 #000000,
      2px 2px 0 #000000;
  }

  .song-pic {
    align-self: center;
  }

  .song-pic img {
    max-width: 50px;
    max-height: 50px;
    margin-right: 2px;
  }

  /* Shake effect on click */
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

  .band img:active {
      animation: shake 0.10s cubic-bezier(.36,.07,.19,.97) both;
  }
  
  @media (min-width: 768px) {
    .clicker {
      display: flex;
      /* justify-content: center; */
    }

    .data {
      align-self: center;
      margin-left: 25px;
    }  
  }
</style>