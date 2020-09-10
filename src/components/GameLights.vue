<template>
  <div class="gameLights">
    <GameButton color="dodgerblue" :size="{wl: 100, wr: 0, dl: 0, dr: 0}" sound="1.mp3" id="0"/>
    <GameButton color="#FF5643" :size="{wl: 0, wr: 100, dl: 0, dr: 0}" sound="2.mp3" id="1"/>
    <GameButton color="#FEEF33" :size="{wl: 0, wr: 0, dl: 100, dr: 0}" sound="3.mp3" id="2"/>
    <GameButton color="#BEDE15" :size="{wl: 0, wr: 0, dl: 0, dr: 100}" sound="4.mp3" id="3"/>
  </div>
</template>

<script>

import GameButton from './GameElement/GameButton';

export default {
  name: 'GameLights',
  components: { GameButton },
};
</script>
<style scoped lang="scss">
  .gameLights{
    width: 200px;
    display: flex;
    flex-wrap: wrap;
  }
</style>
