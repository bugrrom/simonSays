<template>
  <p>Round: {{round}}</p>
</template>
<script>
export default {
  name: 'GameLevel',
  props: {
    round: Number,
  },
};
</script>
<style scoped lang="scss">
  p {
    size: 16px;
    font-weight: bold;
  }
</style>
