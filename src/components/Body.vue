<template>
  <div class="body_main">
    <!-- GIF TAB DISPLAY DIV -->
    <div class="containerTab" v-if="gifTab && showTab">
      <div class="gifTab"  v-for="gif in gifTab" :key="gif.id">
        <img class="imgGif" :src="gif" alt="gif_king" />
      </div>
    </div>
    <div v-if="victory">
      <img class="imageVictory" :src="gifVictory" alt="gif_victory" />
    </div>
    <div class="div_button" v-if="buttonShow">
      <button class="boutton_new_game" @click="newGame(), countDownTimer()">
        nouvelle partie
      </button>
    </div>
    <!-- LUCKY NUMB DIV -->
    <div class="body_lucky_number">
      <div class="lucky_numb_text">
        Choose your lucky number between 0 and 10 (included)
      </div>
      <input type="number" v-model="luckyNumber" id="input_lucky_numb" />
    </div>
    <!-- PLAY ZONE -->
    <div class="body_play_zone">
      <div class="body_click_and_time">
        <button
          id="button_click"
          @click="RandomNumbGenerator(), NumberMatch(), Victory()"
          @click.once="countDownTimer()"
        >
          click
        </button>
        <p class="random_number">{{ this.randomNumber }}</p>
      </div>
      <div class="chrono">
        <p class="chronoTime">
          {{ this.countDown }}
        </p>
      </div>
    </div>
    <!-- SCORES -->
    <div class="container_tab_score" v-if="scoresTab">
      <p class="score_title">Scores:</p>
      <div class="body_scores" v-for="score in scoresTab" :key="score.id">
        <p class="title_scores">{{ score }}</p>
        <div class="tab_scores"></div>
      </div>
    </div>

    <!-- TOTAL -->
    <div class="body_total">
      <p class="total title">Total</p>
      <div class="total_results"></div>
    </div>
  </div>
</template>

<!-- SCRIPT-->
<script>
export default {
  name: "Body",
  data() {
    return {
      /* GAME */
      luckyNumber: "",
      randomNumber: "",
      number: 0,
      gifCharles: require("@/assets/gifs/isolation-charles.gif"),
      gifVictory: require("@/assets/gifs/COURS-DANSE2.gif"),
      victory: false,
      showTab: true,
      buttonShow: false,
      gifTab: [],

      /* CHRONOMETRE */
      countDown: 60,

      /* SCORE */
      scoresTab:[],
      total: 0,
    };
  },

  methods: {
    RandomNumbGenerator() {
      this.randomNumber = Math.floor(Math.random() * 11);
      return this.randomNumber;
    },

    InputValue() {
      this.luckyNumber = document.getElementById("input_lucky_numb").value;
    },

    NumberMatch() {
      if (this.randomNumber == this.luckyNumber) {
        var tabGif = this.gifTab.push(this.gifCharles);
        event.preventDefault();
        return tabGif;
      }
    },
    /* CHRONOMETRE */
    countDownTimer() {
      if (this.countDown > 0 && this.victory == false) {
        setTimeout(() => {
          this.countDown -= 1;
          this.countDownTimer();
        }, 1000);
      }
    },

    Victory() {
      if (this.gifTab.length == 4) {
        this.showTab = false;
        this.victory = true;
        this.gifTab.splice(0);
        this.luckyNumber = "";
        this.randomNumber = "";
        this.buttonShow = true;
        var tabScore = this.scoresTab.push(this.countDown);
        event.preventDefault();
        return tabScore;
      }
    },
    newGame() {
      this.showTab = true;
      this.victory = false;
      this.buttonShow = false;
      this.countDown = 60;
    },
  },
};
</script>

<!-- STYLE -->
<style>
/* TAB GIF */
.containerTab {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.gifTab {
  width: 20%;
}

.body_tab_gifs {
  width: 200px;
  height: 200px;
  margin: 0px;
  padding: 0px;
}
.imgGif {
  width: 80px;
}

/* IMAGE VICTORY */
.imageVictory {
  width: 90%;
}
</style>
