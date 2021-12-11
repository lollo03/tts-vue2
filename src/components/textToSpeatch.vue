<template>
  <div class="textToSpeatch">
    <div class="row">
      <p>Scrivi un testo, dopo {{ tempo }} sec che non scrivi il computer inizierà a parlare. Dopo di che la textbox si cancellerà in automatico.</p>
      <p>Puoi impostare il tempo che il sito aspetterà prima di parlare nello slider in basso</p>
      <div class="left">
        <textarea v-model="userInput" @input="textSpeak()"></textarea>
      </div>
      <div class="right">
        <br />
        <div class="rate-div">
          <div class="label"><b>Velocità : </b> &nbsp;&nbsp;{{ rate }}</div>
          <input class="rate" type="range" min="0.5" max="3" value="1" step="0.1" v-model="rate" @change="salva()" />
        </div>
        <br />
        <div class="pitch-div">
          <div class="label"><b>Intonazione : </b> &nbsp;&nbsp;{{ pitch }}</div>
          <input class="rate" type="range" min="0" max="3" value="1" step="0.1" v-model="pitch" @change="salva()" />
        </div>
        <br />
        <div class="pitch-div">
          <div class="label"><b>Tempo prima di parlare : </b> &nbsp;&nbsp;{{ tempo }} sec</div>
          <input class="rate" type="range" min="0.2" max="3" value="1" step="0.1" v-model="tempo" @change="salva()" />
        </div>
        <button @click="reset()" class="reset">Reset</button>

        <div class="col-12">
          <button id="play" class="parla" type="button" @click="speak()">Avvio manuale</button>
        </div>
      </div>
    </div>
    <br /><br /><br /><br />
  </div>
</template>

<script>
export default {
  name: "textToSpeatch",
  data() {
    let tempo = localStorage.tempo ? localStorage.tempo : 1;
    let rate = localStorage.rate ? localStorage.rate : 1;
    let pitch = localStorage.pitch ? localStorage.pitch : 1;
    return {
      userInput: "",
      pitch,
      rate,
      synth: window.speechSynthesis,
      timer: undefined,
      tempo,
    };
  },
  methods: {
    speak() {
      if (this.synth.speaking) {
        console.error("speechSynthesis.speaking");
        return;
      }
      if (this.userInput !== "") {
        let sInstance = new SpeechSynthesisUtterance(this.userInput);
        sInstance.onend = function(event) {
          console.log("SpeechSynthesisUtterance.onend");
        };

        sInstance.onerror = function(event) {
          console.error("SpeechSynthesisUtterance.onerror");
        };

        sInstance.pitch = this.pitch;
        sInstance.rate = this.rate;
        sInstance.lang = "it-IT";

        this.synth.speak(sInstance);
        this.userInput = "";
      }
    },
    textSpeak(e) {
      clearTimeout(this.timer);

      this.timer = setTimeout(() => {
        this.speak();
      }, this.tempo * 1000);
    },
    salva() {
      localStorage.tempo = this.tempo;
      localStorage.rate = this.rate;
      localStorage.pitch = this.pitch;
    },
    reset() {
      this.tempo = 1;
      this.rate = 1;
      this.pitch = 1;
      this.salva();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.row {
  width: 100%;
  display: block;
}
.row .left {
  width: 100%;
}

.row .right {
  width: 100%;
  font-size: 18px;
}

textarea {
  transition-duration: 0.4s;
  width: 65%;
  height: 150px;
  border: 2px solid;
  padding: 10px;
  font-size: 15px;
  resize: none;
}

textarea:hover {
  border-radius: 15px;
}

textarea:focus {
  border: 2px solid #f2900f;
  border-radius: 15px;
}

.rate {
  width: 60%;
}

.parla {
  margin: 20px;
  transition-duration: 0.4s;
  background-color: #4caf50; /* Green */
  border: 2px solid #4caf50;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 20px;
  cursor: pointer;
}

.parla:hover {
  background-color: white; /* Green */
  color: black;
  border-radius: 15px;
}

.reset {
  transition-duration: 0.4s;
  background-color: white;
  border: 2px solid #f44336;
  color: black;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
}

.reset:hover {
  background-color: #f44336;
  color: white;
  border-radius: 15px;
}
</style>
