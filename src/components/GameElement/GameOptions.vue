<template>
  <div>
    <p>Game options</p>
    <div class="options" >
      <input
        id="1"
        value="1"
        v-model="value"
        v-on:change="$emit('setMode', 1)"
        type="radio"
        :disabled="disabledOptions">
      <label  for="1" >Легкий</label>
    </div>
    <div>
      <input
        id="2"
        value="2"
        v-model="value"
        v-on:change="$emit('setMode', 2)"
        type="radio"
        :disabled="disabledOptions">
      <label for="2">Нормальный</label>
    </div>
    <div>
      <input
        id="3"
        value="3"
        v-model="value"
        v-on:change="$emit('setMode', 3)"
        type="radio"
        :disabled="disabledOptions">
      <label for="3">Сложный</label>
    </div>
  </div>

</template>
<script>
export default {
  data() {
    return {
      value: 1,
    };
  },
  props: {
    disabledOptions: Boolean,
  },
  name: 'GameOptions',
};
</script>
<style scoped lang="scss">
  .options{

  }
</style>
