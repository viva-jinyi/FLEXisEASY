<template>
  <div class="paper" style="min-height: 700px;">
    <button class="containerTag btn-block" :style="containerCSS">
      <button class="boxTag btn-block" v-for="n in boxCnt" :style="boxCSS">Click This!</button>
    </button>
    <span style="display: inline-block; margin: 20px 10px;"><button class="btn-sm">❤</button></span>
  </div>
</template>

<script>
export default {
  name: 'LeftContainter',
  props: {
    containerCSS: "",
    boxCSS: "",
    boxCnt: 0,
  }
}
</script>

<style lang="scss" scoped>
.paper{
  counter-reset: boxTag;
}
.containerTag{
  position: relative;
  width: unset; height: unset;
  padding: 30px;
  &::before{
    content: "Container";
    background-color: #FFF;
    display: inline-block;
    padding: 0 10px;
    position: absolute;
    top: -10px; left: 20px;
    font-weight: bold;
    font-size: 1.15rem;
  }
}
.boxTag{
  counter-increment: boxTag;
  position: relative;
  width: unset; height: unset;
  align-self: unset;
  padding: 25px;
  &::before{
    content:  "Box " counter(boxTag);
    background-color: #FFF;
    display: inline-block;
    padding: 0 10px;
    position: absolute;
    top: -10px; left: 20px;
    font-weight: bold;
    font-size: .9rem;
  }
}
</style>