<template>
  <div class="keys">
    <span v-for="(item,index) in ckeys" :key="index" v-text="item" @click.prevent="handleC(item)"></span>
  </div>
</template>
<script>
export default {
  name: "Container",
  data() {
    return {
        ckeys: ['7', '8', '9', '+', '4', '5', '6', '-', '1', '2', '3', '÷', '0', '.', '=', 'x'],
        theNum: '',
        oldNum: '',
        resultNum: '',
        operator: '',
    }
  },
  mounted () {
      this.$bus.$on('clearAll', () => {
          this.oldNum = ''
          this.theNum = ''
          this.resultNum = ''
      })
  },
  methods: {
      handleC(item) {
          const operators = ['+', '-', 'x', '÷']
          if(/[0-9]/.test(item)) {
              if(this.resultNum) {
                  this.theNum = item
                  this.resultNum = ''
              } else {
                  this.theNum += item
              }
              this.$bus.$emit('changeVal', this.theNum)
          }
          if(operators.includes(item)) {
              this.oldNum = this.theNum
              this.theNum = ''
              this.operator = item
              this.$bus.$emit('changeVal', item)  
          } 
          if(item == '=') {
              let {oldNum,theNum,operator} = this
              if (!oldNum || !theNum) return
              oldNum = parseFloat(oldNum)
              theNum = parseFloat(theNum)
              switch(operator) {
                  case '+':
                      this.resultNum = oldNum + theNum
                      break
                  case '-':
                      this.resultNum = oldNum - theNum
                      break
                  case 'x':
                      this.resultNum = oldNum * theNum
                      break
                  case '÷':
                      this.resultNum = oldNum / theNum
                      break    
                  default:
                      this.resultNum = theNum          
              } 
              this.$bus.$emit('changeVal', this.resultNum)  
              this.oldNum = 0
              this.theNum = this.resultNum 
          }
          if(item == '.') {
              if(this.resultNum) {
                  this.theNum = '0' + item
                  this.$bus.$emit('changeVal', this.theNum)
                  this.resultNum = ''
              } else {
                if(this.theNum.includes(item))  return
                  this.theNum += item
                  this.$bus.$emit('changeVal', this.theNum)
              }
          }
      }
  }
}
</script>
<style lang="css" scoped>
.keys {
    overflow:hidden
}
.keys span {
    float:left;
    position:relative;
    top:0;
    cursor:pointer;
    width:66px;
    height:36px;
    background:#fff;
    border-radius:3px;
    box-shadow:0 4px rgba(0, 0, 0, .2);
    margin:0 7px 11px 0;
    color:#888;
    line-height:36px;
    text-align:center;
    user-select:none;
    transition:all .2s ease
}
.keys span:nth-child(4n) {
    background:#fff0f5;
    margin-right:0
}
.keys span:nth-child(15) {
    background:#f1ff92;
    box-shadow:0 4px #9da853;
    color:#888e5f
}
.keys span:hover {
    background:#9c89f6;
    box-shadow:0 4px #6b54d3;
    color:#fff
}
.keys span.eval:hover {
    background:#abb850;
    box-shadow:0 4px #717a33;
    color:#fff
}
.keys span:active {
    box-shadow:0 0 #6b54d3;
    top:4px
}
.keys span.eval:active {
    box-shadow:0 0 #717a33;
    top:4px
}
</style>