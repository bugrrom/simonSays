<template>
  <div class="home">
    <div class="container">
      <div class="gameHeader">
        <h2>Simon Says</h2>
      </div>
      <div class="game">
        <div>
          <GameLights/>
        </div>
        <div class="gameMenu">
          <GameLevel :round="round"/>
          <button @click="start" :disabled="disabledOptions">Start</button>
          <button @click="restart">Restart</button>
          <GameLoser :gameOver="gameOvers"/>
          <GameOptions v-on:setMode="setMode" :disabledOptions="disabledOptions"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import GameLights from './GameLights';
import GameOptions from './GameElement/GameOptions';
import GameLevel from './GameElement/GameLevel';
import GameLoser from './GameElement/GameLoser';

export default {
  name: 'Home',
  components: {
    GameLoser, GameLevel, GameOptions, GameLights,
  },
  data() {
    return {
      disabledOptions: false,
      round: 0,
      sequence: [],
      mode: 1,
      gameOvers: false,
      state: 'waiting',
    };
  },
  methods: {
    start() {
      this.disabledOptions = true;
      this.gameOvers = false;
      this.newRound();
    },
    restart() {
      this.gameOver();
      this.disabledOptions = false;
      this.round = 0;
      this.sequence = [];
      this.mode = 1;
      this.gameOvers = false;
      this.state = 'waiting';
    },
    newRound() {
      this.round += 1;
      this.sequence = [];

      // eslint-disable-next-line no-plusplus
      for (let i = 0; i < this.round; i++) {
        this.sequence.push(this.randomNumber());
      }
      this.play(this.sequence);
    },
    randomNumber() {
      return Math.floor(Math.random() * 4);
    },
    play(sequence = []) {
      let time = null;
      if (this.mode === 1) {
        time = 1500;
      } else if (this.mode === 2) {
        time = 1000;
      } else {
        time = 400;
      }
      sequence.forEach((n, i) => {
        setTimeout(() => {
          document.querySelectorAll('[data-light-button]')[n].click();
          if (i === sequence.length - 1) {
            this.state = 'listening';
          }
        }, time * i);
      });
    },
    gameOver() {
      this.state = 'gameover';
      this.gameOvers = true;
    },
    setMode(mode) {
      this.mode = mode;
    },
    sequences() {
      return this.sequence;
    },
    shiftSequence() {
      return this.sequence.shift();
    },
    getState() {
      return this.state;
    },
    setState(str) {
      this.state = str;
    },
  },
  mounted() {
    window.$home = this;
  },
};
</script>

<style scoped lang="scss">
  .home{
    width: 100%;
    .container{
      display: flex;
      flex-direction: column;
      .gameHeader{
        display: flex;
        justify-content: center;
      }
      .game{
        display: flex;
        justify-content: center;
        .gameMenu{
          display: flex;
          flex-direction: column;
          justify-content: center;
          align-items: center;
          margin: 0 30px;
          button{
            width: 100px;
            background: greenyellow;
            color: green;
            align-items: center;
            margin: 5px 0;
            padding: 5px;
            border: none;
            border-radius: 5px;
          }
          button:disabled{
            opacity: 0.3;
          }
        }
      }
    }
  }
</style>
