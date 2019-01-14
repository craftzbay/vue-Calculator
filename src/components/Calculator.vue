<template>
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="nemehhasah" class="btn">+/-</div>
    <div @click="huwi" class="btn">%</div>
    <div @click="huwaah" class="btn operator">÷</div>
    <div @click="too('7')" class="btn">7</div>
    <div @click="too('8')" class="btn">8</div>
    <div @click="too('9')" class="btn">9</div>
    <div @click="urjih" class="btn operator">×</div>
    <div @click="too('4')" class="btn">4</div>
    <div @click="too('5')" class="btn">5</div>
    <div @click="too('6')" class="btn">6</div>
    <div @click="hasah" class="btn operator">-</div>
    <div @click="too('1')" class="btn">1</div>
    <div @click="too('2')" class="btn">2</div>
    <div @click="too('3')" class="btn">3</div>
    <div @click="nemeh" class="btn operator">+</div>
    <div @click="too('0')" class="btn zero">0</div>
    <div @click="tseg" class="btn">.</div>
    <div @click="tentsuu" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      omnoh: null,
      current: '',
      operator: null,
      operatorClicked: false
    }
  },
  methods:{
    clear(){
      this.current = ''
    },
    nemehhasah(){
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;

    },
    huwi(){
      this.current = `${parseFloat(this.current)/100 }`;
    },
    tseg(){
      if(this.current.indexOf('.') === -1 ){     this.too('.');     }
    },
    too(number){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;    
    },
    setOmnoh(){
      this.omnoh = this.current;
      this.operatorClicked = true;
    },
    huwaah(){
      this.operator = (a,b) => a/b;
      this.setOmnoh();
    },
    urjih(){
      this.operator = (a,b) => a*b;
      this.setOmnoh();
    },
    nemeh(){
      this.operator = (a,b) => a+b;
      this.setOmnoh();
    },
    hasah(){
      this.operator = (a,b) => a-b;
      this.setOmnoh();
    },
    tentsuu(){
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.omnoh)
      )}`;
      this.omnoh = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator{
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows: minmax(50px,auto);
}
.display{
  grid-column: 1/5;
  background: #333;
  color: white;
}
.zero{
  grid-column: 1/3;
}
.btn{
  background-color: #f2f2f2;
  border: 1px solid #999;
}
.operator{
  background-color: orange;
  color: white;
}
</style>
