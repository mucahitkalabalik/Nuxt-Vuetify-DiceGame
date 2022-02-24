<template>
  <div class="dice-main rounded-xl">
    <section class="player player1">
      <h1 class="player-name">{{player1Name}}</h1>
      <p class="score">{{ diceScore1 }}</p>
      <div
        class="
          score-container
          grey
          white--text
          mt-15
          d-flex
          align-center
          justify-center
          flex-column
          pt-5
          rounded-pill
        "
      >
        <h3>SKOR</h3>
        <p class="current-score">{{ player1Score }}</p>
      </div>
    </section>
    <v-divider vertical></v-divider>
    <section class="player player2">
      <h1 class="player-name">{{player2Name}}</h1>
      <p class="score">{{ diceScore2 }}</p>
      <div
        class="
          score-container
          grey
          white--text
          mt-15
          d-flex
          align-center
          justify-center
          flex-column
          pt-5
          rounded-pill
        "
      >
        <h3>SKOR</h3>
        <p class="current-score">{{ player2Score }}</p>
      </div>
    </section>
    <v-btn
      class="button-groups start"
      outlined
      color="black"
      @click="restartGame"
      >Restart game</v-btn
    >
    <v-btn class="button-groups roll" color="error" @click="changeRoll(player)"
      >roll the dice</v-btn
    >
    <v-btn class="button-groups save" color="warning" @click="save"
      >Save Score</v-btn
    >
         <audio id="audio-player">
        <source
          src="https://file-examples-com.github.io/uploads/2017/11/file_example_MP3_5MG.mp3"
          type="audio/mpeg"
        />
        Your browser does not support the audio tag.
      </audio>
      <v-btn @click="playAudio()" v-if="playBtn" class="play-btn" color="error">
        Music Play
      </v-btn>
      <v-btn
        @click="pauseAudio()"
        v-if="pauseBtn"
        class="play-btn"
        color="error"
        >Music Pause
      </v-btn>
  </div>
</template>

<script>
export default {
  props:{
      player1Name:String,
      player2Name:String,
      gameLine: Boolean
  },
  data() {
    return {
      player: 1,
      diceScore1: 0,
      diceScore2: 0,
      player1Score: 0,
      player2Score: 0,
    };
  },
  computed: {
    parentGameLine: {
      get: function() {
        return this.gameLine;
      },
      set: function(val) {
        this.$emit('update:gameLine',val)
      }
     }
  },
  methods: {
    changeRoll(player) {
      if (player == 1) {
        if (this.diceScore1 == 1) {
          this.player = 2;
          this.diceScore1 = 0;
        } else {
          this.diceScore1 = Math.floor(Math.random() * 6) + 1;
        }
      } else {
        if (player == 2) {
          if (this.diceScore2 == 1) {
            this.diceScore2 = 0;
            this.player = 1;
          } else {
            this.diceScore2 = Math.floor(Math.random() * 6) + 1;
          }
        }
      }
    },
    save() {
      if (this.diceScore1 == 1 || this.diceScore2 == 1) {
        this.diceScore1 = 0;
        this.diceScore2 = 0;
      } else {
        this.player1Score += this.diceScore1;
        this.player2Score += this.diceScore2;
        this.diceScore1 = 0;
        this.diceScore2 = 0;
      }

      if (this.player == 1) this.player = 2;
      else this.player = 1;
    },
    restartGame() {
      this.player1;
      this.player1Score = 0;
      this.player2Score = 0;
      this.parentGameLine=false
    },
    
  },
};
</script>

<style>
.dice-main {
  display: flex;
  background-image: linear-gradient(
    to right,
    #b8cbb8 0%,
    #b8cbb8 0%,
    #b465da 0%,
    #cf6cc9 33%,
    #ee609c 66%,
    #ee609c 100%
  );
  width: 80vw;
  height: 80vh;
  position: relative;
}
.player {
  width: 50%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.player-name {
  margin-bottom: 10rem;
}
.score {
  font-size: 3rem;
}
.current-score {
  font-size: 2rem;
}
.score-container {
  width: 15vw;
}
.button-groups {
  position: absolute !important;
  left: 45%;
}
.start {
  top: 10%;
  left: 44%;
}
.roll {
  top: 60%;
  left: 44%;
}
.save {
  top: 75%;
}
</style>

