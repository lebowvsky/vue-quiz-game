<template>
  <section class="score">
    Player<span>{{ this.winCount }}</span
    >x<span>{{ this.loseCount }}</span
    >Computer
  </section>
  <hr />
</template>
<script>
export default {
  props: {
    winCount: Number,
    loseCount: Number,
  },
};
</script>
<style lang="scss">
.score {
  font-size: 2rem;
  margin: 100px 0 30px 0;
  span {
    display: inline-block;
    padding: 0 5px;
    margin: 0 5px;
    text-align: center;
    border: 1px solid grey;
    font-weight: 700;
  }
}

hr {
  margin: 0 0 50px 0;
}
</style>
