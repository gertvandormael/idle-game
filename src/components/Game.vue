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
        <div class="data">
          <div class="skill">
            <h3>Skill {{ incremental.skill }}</h3>
            <!-- <h3>Cash {{ incremental.cash }} </h3> -->
            <h3>Fame {{ incremental.fame }} </h3>
          </div>
          <div class="stats">
            <h2>Info</h2>
            <ul>
              <li>Click power: {{ incremental.skillPerClick }}</li>
              <li>Idle gain: {{ incremental.idleSkillGain }}</li>
            </ul>
          </div>
        </div>

      </div>
      <div class="instructions">
        <h2>How to play</h2>
        <ul>
          <li>Click the band image to gain more skill</li>
          <li>Songs increase your click power and idle gain</li>
          <li>Shows increase your fame</li>

        </ul>
      </div>
    </div>

    <div class="container">
      <div class="upgrades">
        <h1>Upgrades</h1>
        <div class="song-upgrades">
          <h2>Songs</h2>
          <div class="song">
            <div class="info">
              <div class="pic">
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
              <h3 :class="{ locked: !songUpgrades.disableSong[0] }">
                Smoke On The Water - Deep Purple
              </h3>
            </div>
            <div
              class="button"
              v-if="!songUpgrades.disableSong[0]"
            >
              <button
                @click="learnSong(0)"
                :disabled="skillCheckFirstSong"
              > Learn song!
              </button>
              <div class="requirements">
                <ul>
                  <li>Requires 10 skill</li>
                  <li>Gain 1 click power and 0.5 idle power</li>
                </ul>
              </div>

            </div>
          </div>
          <div class="song">
            <div class="info">
              <div class="pic">
                <img
                  src="../assets/song-locked.png"
                  alt="song locked"
                  v-if="!songUpgrades.disableSong[1]"
                >
                <img
                  src="../assets/song-unlocked.png"
                  alt="song unlocked"
                  v-if="songUpgrades.disableSong[1]"
                >
              </div>
              <h3 :class="{ locked: !songUpgrades.disableSong[1] }">
                Highway to Hell - AC/DC
              </h3>
            </div>
            <div
              class="button"
              v-if="!songUpgrades.disableSong[1]"
            >
              <button
                @click="learnSong(1)"
                :disabled="skillCheckSecondSong"
              >
                Learn song!
              </button>
              <div class="requirements">
                <ul>
                  <li>Requires 50 skill</li>
                  <li>Gain 5 click power and 2 idle power </li>
                </ul>
              </div>
            </div>

          </div>

        </div>

        <!-- <div class="gear-upgrades">
          <h2>Gear</h2>
          <div class="gear">
            <div class="info">
              <div class="pic">
                <img
                  src="../assets/gear-locked.png"
                  alt="gear locked"
                  v-if="!gearUpgrades.disableGear[0]"
                >
                <img
                  src="../assets/gear-unlocked.png"
                  alt="gear unlocked"
                  v-if="gearUpgrades.disableGear[0]"
                >
              </div>
              <h3 :class="{ locked: !gearUpgrades.disableGear[0] }">Line 6 Spider V 30</h3>
            </div>
            <div
              class="button"
              v-if="!gearUpgrades.disableGear[0]"
            >
              <button
                @click="buyGear(0)"
                :disabled="cashCheckFirstGear"
              >
                Buy amp!
              </button>
              <div class="requirements">
                <ul>
                  <li>Requires 100 cash</li>
                  <li>Gain stuff</li>
                </ul>
              </div>
            </div>
          </div>
        </div> -->
      </div>

      <div class="shows">
        <h1>Shows</h1>
        <img
          src="../assets/show-locked.gif"
          alt="show locked"
          v-if="!shows.disableShows[0]"
        >
        <img
          src="../assets/band2.gif"
          alt="show unlocked"
          v-if="shows.disableShows[0]"
        >
        <div class="show">
          <div class="info">
            <h3>Local bar</h3>
          </div>
          <div
            class="button"
            v-if="!shows.disableShows[0]"
          >
            <button
              @click="playShow(0)"
              :disabled="cooldownCheckFirstShow"
            >Play show!</button>
            <div class="requirements">
              <ul>
                <li>Gain {{ fameGain }} fame (20% of your current skill)</li>
              </ul>
            </div>
          </div>
          <div class="cooldown">
            <h3>Duration: {{ shows.durationFirstShow }}</h3>
          </div>

        </div>
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
        disableSong: [false, false]
      },

      gearUpgrades: {
        skill: [1],
        idle: [1],
        disableGear: [false]
      },

      shows: {
        durationFirstShow: 60,
        maximumDurations: [60],
        multiplier: 0.2,
        disableShows: [false, false]
      },
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
    },

    cashCheckFirstGear() {
      if (this.incremental.cash < 100) {
        return true;
      } else {
        return false;
      }
    },

    cooldownCheckFirstShow() {
      if (this.shows.durationFirstShow === this.shows.maximumDurations[0]) {
        return false;
      } else {
        return true;
      }
    },

    fameGain() {
      return Math.round(this.incremental.skill * this.shows.multiplier);
    }
  },

  methods: {
    increaseSkill() {
      this.incremental.skill += this.incremental.skillPerClick;
    },

    idleGains() {
      setInterval(() => {
        this.incremental.skill += this.incremental.idleSkillGain;
      }, 1000);
    },

    learnSong(number) {
      this.incremental.skillPerClick += this.songUpgrades.skill[number];
      this.incremental.idleSkillGain += this.songUpgrades.idle[number];
      this.songUpgrades.disableSong[number] = true;
    },

    buyGear(number) {
      this.incremental.cash -= 100;
      this.incremental.skillPerClick += this.gearUpgrades.skill[number];
      this.incremental.idleSkillGain += this.gearUpgrades.idle[number];
      this.gearUpgrades.disableGear[number] = true;
    },

    playShow(number) {
      this.incremental.fame += Math.round(
        this.incremental.skill * this.shows.multiplier
      );
      this.incremental.cash += 100;
      this.shows.disableShows[number] = true;
      this.showCooldown(number);
    },

    showCooldown(number) {
      this.shows.disableShows[number] = true;
      if (this.shows.durationFirstShow > 0) {
        setTimeout(() => {
          --this.shows.durationFirstShow;
          this.showCooldown(number);
        }, 1000);
      } else {
        this.shows.disableShows[number] = false;
        this.shows.durationFirstShow = this.shows.maximumDurations[number];
      }
    }
  },

  mounted() {
    this.idleGains();
  },
};
</script>

<style>
/* Component specific layout */
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





  

  .info, .button {
    display: flex;
  }

  .info h3 {
    align-self: center;
  }
  
  .requirements {
    align-self: center;
  }

  .locked {
    color: #dadada;
    text-shadow:
      -2px -2px 0 #000000,
      2px -2px 0 #000000,
      -2px 2px 0 #000000,
      2px 2px 0 #000000;
  }

  .pic {
    align-self: center;
  }

  .pic img {
    max-width: 50px;
    max-height: 50px;
    margin-right: 2px;
  }

  .buttonCooldown {
    background: red;
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
      .band {
        display: flex;
        justify-content: center;
      }

    .clicker {
      display: flex;
      justify-content: space-between;
    }

    .data {
      /* align-self: center; */
      margin-left: 25px;
    } 

    .instructions {
      width: 350px;
    }

  }

  @media (min-width: 996px) {

    .container {
      display: flex;
    }

    .upgrades {
      width: 500px;
    }

    .shows {
      width: 400px;
    }
  }

</style>