<template>
  <div class="body_main">
    <!-- GIF TAB DISPLAY DIV -->
    <div class="containerTab" v-if="gifTab && showTab">
      <div class="gifTab" v-for="gif in gifTab" :key="gif.id">
        <img class="imgGif" :src="gif" alt="gif_king" />
      </div>
    </div>
    <div class="div_victory" v-if="victory">
      <img class="imageVictory" :src="gifVictory" alt="gif_victory" />
    </div>
    <div class="div_button" v-if="buttonShow">
      <button class="boutton_new_game" @click="newGame(), countDownTimer()">
        start new game
      </button>
    </div>

    <!-- LUCKY NUMB DIV -->
    <div class="body_play_zone">
      <div class="body_lucky_number">
        <div class="lucky_numb_text">
          Write your lucky number between 0 and 10 (included)
        </div>
        <div class="input_lucky_number_container">
          <input
            class="input_number"
            type="number"
            v-model="luckyNumber"
            id="input_lucky_numb"
          />
        </div>
      </div>
      <!-- PLAY ZONE -->
      <div class="body_click_and_time">
        <div class="button_click_container">
          <button
            id="button_click"
            @click="RandomNumbGenerator(), NumberMatch(), Victory()"
            @click.once="countDownTimer()"
          >
            click
          </button>
        </div>
        <div class="div_random_number">
          <p class="random_number">{{ this.randomNumber }}</p>
        </div>
      </div>
      <div class="chrono">
        <p class="chronoTime">
          CountDown:
          {{ this.countDown }}
        </p>
      </div>
    </div>

    <!-- SCORES -->
    <div class="container_score" v-if="scoresTab">
      <div class="container_title_score">
        <p class="score_title">Scores</p>
      </div>
      <div class="body_score_container">
        <div
          class="div_boucle_scores"
          v-for="score in scoresTab"
          :key="score.id"
        >
          <div class="tab_scores">{{ score }}</div>
        </div>
      </div>
    </div>

    <!-- TOTAL -->
    <div class="body_total" v-if="total" v-bind="Total()">
      <p class="total title">Total:</p>
      <div class="total_results">{{ this.total }}</div>
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
      scoresTab: [],
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
      this.countDown = 30;
    },

    /* CALCUL TOTAL */
    Total() {
      if (this.scoresTab.length == 3) {
        for (let i = 0; i < this.scoresTab.length; i++) {
          this.total += this.scoresTab[i];
        }
        return this.total;
      }
    },
  },
};
</script>

<!-- STYLE -->
<style>
@font-face {
  font-family: "Roman";
  src: local("Roman SD"), url(../assets/font/RomanSD.ttf) format("truetype");
}
@font-face {
  font-family: "Tratatello";
  src: local("Tratatello"),
    url(../assets/font/Trattatello.ttf) format("truetype");
}
.body_main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  right: 0px;
  left: 0px;
  top: 0px;
  bottom: 0px;
}

/* TAB GIF */
.containerTab {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.gifTab {
  width: 20%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
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
.div_victory {
  width: 62%;
  display: flex;
  flex-direction: row;
  justify-content: center;
}
/* BOUTON NEW GAME */
.boutton_new_game {
  margin-top: 30px;
  width: 250px;
  height: 30px;
  color: black;
  font-family: "Roman";
  font-size: 15px;
  background: #657634;
  border: 2px solid #a5920f;
  border-radius: 5px;
}
/* PLAYZONE */
.body_play_zone {
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* lucky number */
.body_lucky_number {
  width: 400px;
  margin-top: 10px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.lucky_numb_text {
  width: 50%;
  text-align: left;
  color: #a5920f;
  font-family: "Roman";
  font-size: 15px;
}
.input_lucky_number_container {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: #a5920f;
  border: 0px;
}
#input_lucky_numb {
  position: absolute;
  text-align: center;
  width: 50px;
  height: 50px;
  background: none;
  border-radius: 50%;
  color: black;
  font-family: "Tratatello";
  font-size: 30px;
}

/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type="number"] {
  -moz-appearance: textfield;
}

/* CLICK */
.body_click_and_time {
  width: 400px;
  margin-top: 10px;
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.button_click_container {
  width: 50%;
  display: flex;
  flex-direction: row;
  align-items: center;
}

#button_click {
  width: 150px;
  height: 30px;
  color: black;
  font-family: "Roman";
  font-size: 15px;
  background: #a5920f;
  border: 2px solid #a5920f;
  border-radius: 5px;
}
.div_random_number {
  position: relative;
  display: flex;
  justify-content: center;
  align-content: center;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: #657634;
  border: 0px;
  color: black;
  font-family: "Tratatello";
  font-size: 30px;
}
.random_number {
  margin: 0px;
  text-align: center;
  display: flex;
  justify-content: center;
  align-content: center;
}
/* CHRONO */
.chrono {
  width: 62%;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  color: #a5920f;
  font-family: "Roman";
  font-size: 15px;
}
/* SCORE */
.container_score {
  width: 400px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0px;
  color: #a5920f;
  font-family: "Roman";
}

.container_title_score {
  width: 62%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  border-radius: 10px 10px 0px 0px;
  border: 1px solid #a5920f;
  font-size: 30px;
}

.body_score_container {
  width: 62%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  border-radius: 0px 0px 10px 10px;
  border: 1px solid #a5920f;
  background-color: #a5920f;
}

.tab_scores {
  margin: 10px 10px 10px 0px;
  font-family: "Roman";
  color: black;
  font-size: 20px;
}
</style>
