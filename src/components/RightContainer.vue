<template>
  <div style="min-height: 700px; padding: 20px; position: relative;">
    
    <div style="display: flex; margin-bottom: 50px;">
      <h3 class="tab plum" :class="{ 'highlight': !controlBox }" style="margin-right: 20px;"><b style="color: #FFF;" @click="controlBox=false">container</b></h3>
      <h3 class="tab plum" :class="{ 'highlight': controlBox }"><b style="color: #FFF;" @click="controlBox=true">box</b></h3>
    </div>

    <div v-if="!controlBox">
      <div style="margin: 0 12px 12px 12px;">
        <span style="color: #FFF; font-size: 1.2rem; font-weight: bold; margin-right: 15px;">width</span>
        <input v-model="containerWidth" @change="onEmitContanier" type="number" min="0" style="background-color: #FFF; width: 80px;"><span style="color: #FFF"> %</span>
      </div>
      <div style="margin: 0 12px 12px 12px;">
        <span style="color: #FFF; font-size: 1.2rem; font-weight: bold; margin-right: 15px;">height</span>
        <input v-model="containerHeight" @change="onEmitContanier" type="number" min="0" style="background-color: #FFF; width: 80px;"><span style="color: #FFF"> px</span>
      </div>
      <div v-for="setting in containerSetting" style="margin: 0 12px 12px 12px;">
        <span style="color: #FFF; font-size: 1.2rem; font-weight: bold; margin-right: 15px;">{{ setting.select }}</span>
        <select @change="onEmitContanier" style="background-color: #FFF;" v-model="setting.model">
          <option v-for="option in setting.options" :value="option">{{ option }}</option>
        </select>
      </div>
      <div style="margin: 0 12px 12px 12px;">
        <span style="color: #FFF; font-size: 1.2rem; font-weight: bold; margin-right: 15px;">gap</span>
        <input v-model="gapY" @change="onEmitContanier" type="number" min="0" style="background-color: #FFF; width: 80px;"><span style="color: #FFF"> px</span>
        <input v-model="gapX" @change="onEmitContanier" type="number" min="0" style="background-color: #FFF; width: 80px; margin-left: 10px;"><span style="color: #FFF"> px</span>
      </div>
      <div v-if="containerSetting[2].model==='wrap'" style="margin: 0 12px 12px 12px;">
        <span style="color: #FFF; font-size: 1.2rem; font-weight: bold; margin-right: 15px;">align-content</span>
        <select @change="onEmitContanier" style="background-color: #FFF;" v-model="alignContent">
          <option value="stretch">stretch</option>
          <option value="flex-start">flex-start</option>
          <option value="flex-end">flex-end</option>
          <option value="center">center</option>
          <option value="space-between">space-between</option>
          <option value="space-around">space-around</option>
          <option value="space-evenly">space-evenly</option>
        </select>
      </div>
    </div>

    <div v-else>
      <label style="margin: 0 12px 12px 12px; display: block; user-select: none;">
        <input v-model="specifyPX" @change="onEmitBox" type="checkbox" style="display: inline-block; margin-right: 25px;">
        <span style="color: #FFF; font-size: 1rem; font-weight: bold; margin-right: 15px;">I need to specify width / height.</span>
      </label>
      <div style="margin: 0 12px 12px 12px;">
        <span style="color: #FFF; font-size: 1.2rem; font-weight: bold; margin-right: 15px;">box</span>
        <input v-model="boxCnt" @change="onEmitBox" type="number" min="1" style="background-color: #FFF; width: 60px;">
      </div>
      <div v-if="specifyPX" style="margin: 0 12px 12px 12px;">
        <span style="color: #FFF; font-size: 1.2rem; font-weight: bold; margin-right: 15px;">width</span>
        <input v-model="boxWidth" @change="onEmitBox" type="number" min="0" style="background-color: #FFF; width: 80px;"><span style="color: #FFF"> %</span>
      </div>
      <div v-if="specifyPX" style="margin: 0 12px 12px 12px;">
        <span style="color: #FFF; font-size: 1.2rem; font-weight: bold; margin-right: 15px;">height</span>
        <input v-model="boxHeight" @change="onEmitBox" type="number" min="0" style="background-color: #FFF; width: 80px;"><span style="color: #FFF"> %</span>
      </div>
      <div style="margin: 0 12px 12px 12px;">
        <span style="color: #FFF; font-size: 1.2rem; font-weight: bold; margin-right: 15px;">flex-basis</span>
        <select @change="onEmitBox" style="background-color: #FFF; margin-right: 5px;" v-model="flexBasis">
          <option value="auto">auto</option>
          <option value="content">content</option>
          <option value="custom">CUSTOMIZE ✍</option>
        </select>
        <label v-if="flexBasis==='custom'">
          <input v-model="customBasis" @change="onEmitBox" type="number" min="0" style="background-color: #FFF; width: 80px;"><span style="color: #FFF"> %</span>
        </label>
      </div>
      <div style="margin: 0 12px 12px 12px;">
        <span style="color: #FFF; font-size: 1.2rem; font-weight: bold; margin-right: 15px;">flex-grow</span>
        <select @change="onEmitBox" style="background-color: #FFF;" v-model="flexGrow">
          <option value="0">0</option>
          <option value="1">1</option>
        </select>
      </div>
    </div>
    
    <label class="paper-btn" style="margin-top: 50px; max-width: 350px; text-align: center; width: 100%; position: absolute; bottom: 20px; left: 20px;" for="modal-1">Get Code 💻</label>
    <input class="modal-state" id="modal-1" type="checkbox">
    <div class="modal">
      <label class="modal-bg" for="modal-1"></label>
      <div class="modal-body" style="min-width: 450px;">
        <label class="btn-close" for="modal-1">X</label>
        <p class="modal-text">
          <p style="line-height: 1.7">
            .container{
              <span v-html="css_1"></span><br>
            }<br>
            .box{<span v-html="css_2"></span><br>
            }
        </p>
        <label class="paper-btn" for="modal-1" @click="copyToClipboard">Copy ❤</label>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      controlBox: false,
      containerWidth: 90,
      containerHeight: 500,
      gapY: 0,
      gapX: 0,
      alignContent: "stretch",
      containerSetting: [
        {
          select: "display",
          options: ["flex", "inline-flex"],
          model: "flex"
        },
        {
          select: "flex-direction",
          options: ["row", "column", "row-reverse", "column-reverse"],
          model: "row"
        },
        {
          select: "flex-wrap",
          options: ["nowrap", "wrap", "wrap-reverse"],
          model: "nowrap"
        },
        {
          select: "justify-content",
          options: ["flex-start", "flex-end", "center", "space-between", "space-around", "space-evenly"],
          model: "flex-start"
        },
        {
          select: "align-items",
          options: ["stretch", "flex-start", "flex-end", "center", "baseline"],
          model: "flex-start"
        },
      ],
      boxCnt: 3,
      specifyPX: false,
      boxWidth: 30,
      boxHeight: 30,
      flexBasis: 'auto',
      flexGrow: 0,
      customBasis: 25,
      css_1: '',
      css_2: ''
    }
  },
  created () {
    this.onEmitContanier();
    this.onEmitBox();
  },
  methods: {
    onEmitContanier() {
      if(this.containerSetting[2].model==='wrap'){
        let css = `
          width: ${this.containerWidth}%;
          height: ${this.containerHeight}px;
          display: ${this.containerSetting[0].model};
          flex-direction: ${this.containerSetting[1].model};
          flex-wrap: ${this.containerSetting[2].model};
          justify-content: ${this.containerSetting[3].model};
          align-items: ${this.containerSetting[4].model};
          gap: ${this.gapY}px ${this.gapX}px;
          align-content: ${this.alignContent};`
        this.css_1 = css.replace(/\n/g, "<br>");
        css = css.replace(/\n/g, "");
        this.$emit("setContainer",css)
      }else{
        let css = `
          width: ${this.containerWidth}%;
          height: ${this.containerHeight}px;
          display: ${this.containerSetting[0].model};
          flex-direction: ${this.containerSetting[1].model};
          flex-wrap: ${this.containerSetting[2].model};
          justify-content: ${this.containerSetting[3].model};
          align-items: ${this.containerSetting[4].model};
          gap: ${this.gapY}px ${this.gapX}px;`
        this.css_1 = css.replace(/\n/g, "<br>");
        css = css.replace(/\n/g, "");
        this.$emit("setContainer", css)
      }
      const regex = / /gi;
      this.cssCode = `.container{
          ${this.css_1.replace(/<br>/ig, "").replace(regex, '')}
        }
        .box{
          ${this.css_2.replace(/<br>/ig, "").replace(regex, '')}
        }`
    },
    onEmitBox() {
      let basisCSS = this.flexBasis === 'custom' ? `flex-basis: ${this.customBasis}%;` : `flex-basis: ${this.flexBasis};`; 
      if(!this.specifyPX){
        let css = `
          flex-grow: ${this.flexGrow};
        ` + basisCSS
        this.css_2 = css.replace(/\n/g, "<br>");
        css = css.replace(/\n/g, "");
        this.$emit("setBox", css)
        this.$emit("setBoxCnt", Number(this.boxCnt))
      }else{
        let css = `
          width: ${this.boxWidth}%;
          height: ${this.boxHeight}%;
          flex-grow: ${this.flexGrow};
        ` + basisCSS
        this.css_2 = css.replace(/\n/g, "<br>");
        css = css.replace(/\n/g, "");
        this.$emit("setBox", css)
        this.$emit("setBoxCnt", Number(this.boxCnt))
      }
    },
    copyToClipboard() {
      let tempElem = document.createElement('textarea');
      let containerCss = this.css_1;
      let boxCss = this.css_2;
      const regex = / /gi;
      tempElem.value = `.container{
        ${containerCss.replace(/<br>/ig, "").replace(regex, '')}
      }
      .box{
        ${boxCss.replace(/<br>/ig, "").replace(regex, '')}
      }`
      document.body.appendChild(tempElem);

      tempElem.select();
      document.execCommand("copy");
      document.body.removeChild(tempElem);
    }
  }
}
</script>

<style lang="scss" scoped>
.tab{
  cursor: pointer;
  user-select: none;
}
</style>