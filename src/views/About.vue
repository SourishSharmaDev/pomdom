<template>
  <div class="about">
    <section>
      <div class="center">
        <div class="quote">
          <h3>{{ quotes[randQuote].q }}</h3>
          <span>{{ quotes[randQuote].c }}</span>
        </div>
        <div class="timer">
          <p id="countdown">{{ countdown }}</p>
          <!-- <progress :value = 'progTime' :max = 'progTotTime'/> -->
        </div>
        <button class="but" @click="start" v-show="!isClicked">start</button>
        
        <button class="red-but" @click="reset" v-show="isClicked">quit session</button>

        <br><br>
        <div class="nex" v-if="isBreak">
          <transition name="fade">
            <b><router-link class="next"  to="/"> >> </router-link></b>
          </transition>
        </div>
      </div>
      <div class="wave wave1"></div>
      <div class="wave wave2"></div>
      <div class="wave wave3"></div>
      <div class="wave wave4"></div>
    </section>
  </div>
</template>
<script>
import { ref } from "@vue/reactivity";
export default {
  name: "About",
  setup() {
    const startTime = 5;
    let time = startTime * 60;
    const progTime = ref(startTime * 60);
    const progTotTime = ref(startTime * 60);
    const countdown = ref("5:00");
    let isClicked = ref(false);
    const isBreak = ref(false);
    const quotes = ref([
      {
        q:
          "Concentrate all your thoughts upon the work in hand. The sun's rays do not burn until brought to a focus",
        c: "Alexander Graham Bell",
      },
      { q: "Either you run the day or the day runs you.", c: "Jim Rohn" },
      {
        q:
          "I’m a greater believer in luck, and I find the harder I work the more I have of it",
        c: "Thomas Jefferson",
      },
      {
        q:
          "When we strive to become better than we are, everything around us becomes better too",
        c: "Paulo Coelho",
      },
      {
        q:
          "Opportunity is missed by most people because it is dressed in overalls and looks like work",
        c: "Thomas Edison",
      },
      {
        q:
          "You've got to get up every morning with determination if you're going to go to bed with satisfaction",
        c: "George Lorimer",
      },
      {
        q:
          "Don’t judge each day by the harvest you reap but by the seeds that you plant",
        c: "Robert Louis Stevenson",
      },
      {
        q:
          "Just one small positive thought in the morning can change your whole day",
        c: "Dalai Lama",
      },
      {
        q: "Whether you think you can, or you think you can’t – you’re right",
        c: "Henry Ford",
      },
      { q: "Don’t wish it were easier. Wish you were better", c: "Jim Rohn" },
      {
        q: "Do the hard jobs first. The easy jobs will take care of themselves",
        c: "Dale Carnegie",
      },
      { q: "The future depends on what you do today", c: "Mahatma Gandhi" },
      {
        q: "The man who moves a mountain begins by carrying away small stones",
        c: "Confucius",
      },
    ]);
    const randQuote = ref(Math.floor(Math.random() * quotes.value.length));
    let inter;

    const timer = () => {
      const Minutes = Math.floor(time / 60);
      let sec = time % 60;

      sec = sec < 10 ? "0" + sec : sec;

      countdown.value = `${Minutes}:${sec}`;
      time--;
      progTotTime.value = time;
      time = time < 0 ? 0 : time;

      if (time == 0) {
        isBreak.value = true;
      }
    };

    const start = () => {
      if (isClicked.value == false) {
        inter = setInterval(timer, 1000);
        isClicked.value = true;
      }
    };

    const reset = () => {
      isClicked.value = false;
      clearInterval(inter);
      countdown.value = "5:00";
      time = startTime * 60;
    };
    return { quotes, randQuote, countdown, start, isBreak, reset, isClicked, progTime, progTotTime };
  },
};
</script>
<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Rokkitt&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.next{
  font-size: 20px;
  text-decoration: none;
  background: #7AC5FC;
  padding: 5px 30px;
  color:black;
  border-radius: 20px 5px ;
}

.center {
  text-align: center;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

section {
  position: relative;
  width: 100%;
  font-family: 'Rokkitt', serif;
  height: 100vh;
  background: #24a658;
  overflow: hidden;
}

section .timer #countdown{
  font-size: 100px;
  color: aliceblue;
}

section .but, .red-but {
  font-size: 20px ;
  padding: 5px 30px;
  border: none;
  border-radius: 5px;
}

.but{
  background: #C4C4C4;
}

.red-but{
  background: rgb(235, 101, 101);
}

section .wave {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100px;
  background: url(../assets/wave.png);
  background-size: 1000px 100px;
}


section .wave.wave1 {
  animation: animate2 15s linear infinite;
  z-index: 1000;
  opacity: 1;
  animation-delay: 0s;
  bottom: 0;
}

section .wave.wave2 {
  animation: animate 30s linear infinite;
  z-index: 1000;
  opacity: 0.5;
  animation-delay: -5s;
  bottom: 10px;
}

section .wave.wave3 {
  animation: animate 30s linear infinite;
  z-index: 998;
  opacity: 0.2;
  animation-delay: -2s;
  bottom: 15px;
}

section .wave.wave4 {
  animation: animate2 5s linear infinite;
  z-index: 997;
  opacity: 0.7;
  animation-delay: -5s;
  bottom: 20px;
}

@keyframes animate {
  0% {
    background-position-x: 0;
  }
  100% {
    background-position-x: 1000px;
  }
}

@keyframes animate2 {
  0% {
    background-position-x: 0;
  }
  100% {
    background-position-x: -1000px;
  }
}
</style>
