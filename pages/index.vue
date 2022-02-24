<template>
  <div class="home-container">
    <div v-if="!gameLine" class="main-home">
      <div class="input-container">
        <v-text-field
          color="white"
          label="Player 1 Name"
          v-model="player1Name"
        ></v-text-field>
        <v-text-field
          color="white"
          label="Player 2 Name"
          v-model="player2Name"
        ></v-text-field>
        <v-btn outlined color="white" @click="gameLine = true"
          >Start Game</v-btn
        >
      </div>
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

    <mainDice
      v-if="gameLine"
      :player1Name="player1Name"
      :player2Name="player2Name"
      :gameLine.sync="gameLine"
    />
  </div>
</template>

<script>
import mainDice from "../components/mainDice.vue";
export default {
  components: {
    mainDice,
  },
  data() {
    return {
      player1Name: null,
      player2Name: null,
      pauseBtn: false,
      playBtn: true,
      gameLine: false,
    };
  },
  methods: {
    playAudio() {
      var audio = document.getElementById("audio-player");
      audio.play();
      this.pauseBtn = true;
      this.playBtn = false;
    },
    pauseAudio() {
      var audio = document.getElementById("audio-player");
      audio.pause();
      this.playBtn = true;
      this.pauseBtn = false;
    },
  },
};
</script>

<style>
.home-container {
  background-color: #21d4fd;
  background-image: linear-gradient(19deg, #21d4fd 0%, #b721ff 100%);

  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.main-home {
  width: 80vw;
  height: 80vh;
  background-color: rgba(255, 255, 255, 0.356);
  border-radius: 2rem;
  padding: 10rem;
  position: relative;
}
.play-btn {
  position: absolute;
  top: 0%;
  right: 0;
}
.container-dice {
  background-image: linear-gradient(to top, #30d0d06b 0%, #33086763 100%);
  height: 100vh;
  widows: 100vw;
}
</style>