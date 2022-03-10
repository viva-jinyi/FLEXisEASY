<template>
  <div style="padding: 0 min(40px, 5vw);">
    <common-header></common-header>
    <div class="wrapper">
      <left-container class="left" :containerCSS="containerCSS" :boxCSS="boxCSS" :boxCnt="boxCnt"></left-container>
      <right-container class="right" @setContainer="setContainer" @setBox="setBox" @setBoxCnt="setBoxCnt"></right-container>
    </div>
  </div>
</template>

<script>
import CommonHeader from '@/components/CommonHeader.vue'
import LeftContainer from '@/components/LeftContainer.vue'
import RightContainer from '@/components/RightContainer.vue'

export default {
  components: { CommonHeader, LeftContainer, RightContainer },
  name: 'Main',
  data() {
    return {
      containerCSS: '',
      boxCSS: '',
      boxCnt: 0,
    }
  },
  methods: {
    setContainer(value) {
      this.containerCSS = value;
    },
    setBox(value) {
      this.boxCSS = value;
    },
    setBoxCnt(value) {
      this.boxCnt = value;
    },
  },
}
</script>
<style lang="scss" scoped>
.wrapper{
  display: flex;
  gap: 15px;
  @media only screen and (max-width: 920px) {
    & {
      flex-direction: column;
    }
  }
}
.left{
  width: 65%;
  @media only screen and (max-width: 920px) {
    & {
      width: 100%;
    }
  }
}
.right{
  width: 35%;
  @media only screen and (max-width: 920px) {
    & {
      width: 100%;
    }
  }
}
</style>
