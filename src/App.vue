<template>
  <div id="app">
    <div class="text-to-speech">
      <h1>Text to speech</h1>
      <textToSpeech />
    </div>
    <div class="footer">
      <p>Creato con &hearts; da Lorenzo Andreasi (<a href="https://github.com/lollo03">GitHub</a>)</p>
      <span class="text-muted">Copyleft <span class="copyleft">&copy;</span> Lorenzo Andreasi, 2021. <i>Some rights reserved.</i></span> <br />
    </div>
  </div>
</template>

<script>
import textToSpeech from "./components/textToSpeech.vue";

export default {
  name: "app",
  components: {
    textToSpeech,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
  margin-top: 60px;
}
.footer {
  font-size: small;
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  text-align: center;
  color: white;
  background-color: #2c3e50;
  padding-bottom: 5px;
  margin-top: 30px;
}
.footer a {
  color: orange;
}

.copyleft {
  display: inline-block;
  transform: rotate(180deg);
}
</style>
