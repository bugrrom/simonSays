<template>
  <div class="gameLightsButton">
      <button
        ref="btn"
        :data-light-button = "id"
        @click="click($event)"
        :style="{backgroundColor:`${color}`, borderRadius:`${size.wl}`+'px'+' '+ `${size.wr}`+'px'+' '+ `${size.dr}`+'px'+' '+ `${size.dl}`+'px'}">

      </button>
  </div>
</template>

<script>
export default {
  name: 'GameButton',
  props: {
    color: {
      type: String,
    },
    sound: {
      type: String,
    },
    size: {
      type: Object,
    },
    id: {
      type: String,
    },
  },
  methods: {
    click($event) {
      const turn = window.$home.getState();
      if (turn !== 'listening' && (!$event || $event.isTrusted)) {
        return;
      }
      const $btn = this.$refs.btn;
      $btn.classList.add('click');
      const key = $btn?.dataset?.lightButton;
      setTimeout(() => { $btn.classList.remove('click'); }, 200);
      // eslint-disable-next-line global-require,import/no-dynamic-require
      this.playSound(require(`@/assets/sound/${this.sound}`));
      this.checkSequence(key);
    },
    playSound(sound) {
      const audio = new Audio(sound);
      audio.play();
    },
    checkSequence(key) {
      if (window.$home.getState() === 'listening') {
        const expected = window.$home.shiftSequence();
        if (String(expected) === String(key)) {
          if (!window.$home.sequences().length) {
            setTimeout(() => {
              if (window.$home.getState() === 'gameover') return;
              window.$home.setState('waiting');
              window.$home.newRound();
            }, 1000);
          }
        } else {
          window.$home.gameOver();
        }
      }
    },
  },
};
</script>
<style scoped lang="scss">
  .gameLightsButton{
    width: 100px;
    height: 100px;
    button{
      width: 100%;
      height: 100%;
      cursor: pointer;
      border: none;
      outline:none;
      opacity: 0.5;
    }
    .click{
      border: none;
      opacity: 1;
    }
  }
</style>
