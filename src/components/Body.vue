<template>
  <div class="body_main">
    <!-- GIF TAB DISPLAY DIV -->
    <div class="body_tab_gifs"> {{this.gifTab}} </div>
    <!-- LUCKY NUMB DIV -->
    <div class="body_lucky_number">
      <div class="lucky_numb_text">
        Choose your lucky number between 0 and 10 (included)
      </div>
      <input type="number" v-model="luckyNumber" id="input_lucky_numb"/>
    </div>
    <!-- PLAY ZONE -->
    <div class="body_play_zone">
      <div class="body_click_and_time">
        <button id="button_click" @click='RandomNumbGenerator(), NumberMatch()'>click</button>
        <p class="random_number">{{this.randomNumber}}</p>
      </div>
      <div class="chrono"></div>
    </div>
    <!-- SCORES -->
    <div class="body_scores">
      <p class="title_scores">Scores</p>
      <div class="tab_scores"></div>
    </div>
    <div class="body_total">
      <p class="total title">Total</p>
      <div class="total_results"></div>
    </div>
  </div>
</template>

<!-- SCRIPT-->
<script>
export default {
    name:'Body',
    data() {
        return {
            luckyNumber:'',
            randomNumber:'',
            number: 0,
            gifHenri:2,
            gifTab:[],
            scoresTab:[],
            total:0,
        }
    },

        methods: {
            RandomNumbGenerator(){
                this.randomNumber =  Math.floor(Math.random()*11);
                return this.randomNumber
            },

            InputValue(){
                this.luckyNumber = document.getElementById("input_lucky_numb").value;
            },

            NumberMatch(){
                if(this.randomNumber == this.luckyNumber){
                  var tabGif = this.gifTab.push(this.gifHenri)
                  return tabGif
                }
            }
        },
};
</script>

<!-- STYLE -->
<style></style>
