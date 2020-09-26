<template>
  <div class="top">
    <span class="clear" @click="clearVal">C</span>
    <div class="screen" v-text="inputVal"></div>
  </div>
</template>
<script>
export default {
  name: "Header",
  data() {
    return {
        inputVal: ''
    }
  },
  mounted () {
      this.$bus.$on('changeVal', (inputVal) => {
          this.inputVal = inputVal
      })
  },
  methods: {
      clearVal() {
          this.inputVal = ''
          this.$bus.$emit('clearAll')
      }
  }
}
</script>
<style lang="css" scoped>
.top {
  overflow: hidden;
}
.top .clear {
    float:left;
    background: #ff9fa8;
    box-shadow:0 4px #ff7c87;
    color: #fff;
    position:relative;
    top:0;
    cursor:pointer;
    width:66px;
    height:36px;
    border-radius:3px;
    margin:0 7px 11px 0;
    line-height:36px;
    text-align:center;
    user-select:none;
    transition:all .2s ease
}
.top span.clear:hover {
    background:#f68991;
    box-shadow:0 4px #d3545d;
    color:#fff
}
.top span.clear:active {
    top:4px;
    box-shadow:0 0 #d3545d
}
.top .screen {
    height:40px;
    width:212px;
    float:right;
    padding:0 10px;
    background:rgba(0, 0, 0, .2);
    border-radius:3px;
    box-shadow:inset 0 4px rgba(0, 0, 0, .2);
    font-size:17px;
    line-height:40px;
    color:#fff;
    text-shadow:1px 1px 2px rgba(0, 0, 0, .2);
    text-align:right;
    letter-spacing:1px
}
</style>