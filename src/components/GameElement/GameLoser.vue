<template>
  <div class="over" v-if="gameOver">Вы проиграли</div>
</template>
<script>
export default {
  name: 'GameLoser',
  props: {
    gameOver: Boolean,
  },
};
</script>
<style scoped lang="scss">
  .over{
    width: 100px;
    padding: 5px;
    margin: 5px 0;
    background-color: red;
    color: white;
    font-size: 14px;
    font-weight: bold;
    border-radius: 5px;
  }
</style>
