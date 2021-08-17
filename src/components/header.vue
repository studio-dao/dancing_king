<template>
  <header class="header">
    <div class="title_cligno">
      <img
        class="app_title"
        src="../assets/jpg/app_title.png"
        alt="app_title"
      />
      <img
        class="ligne_cligno"
        src="../assets/jpg/ligne_cligno.png"
        alt="cligno"
      />
    </div>
    <div class="div_text_intro">
    <p class="head_texte_intro">
      Choose a number, click fast, if you make numbers match within 30s, you win
      !
    </p>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style>
.header{
  margin-top: 20px;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.app_title {
  width: 75%;
}
.title_cligno {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.ligne_cligno {
  position: absolute;
  top: 50%;
  width: 70%;
}
.div_text_intro{
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-content: center;
  text-align: center;
  width: 62%;
  margin: 0px;
  font-family: "Tratatello";
  color: #a5920f;
}
</style>
