<template>
  <div class="calculator">
    <div class="display"> <div class="result"> {{current || '0'}} </div> </div>
    <button @click="clear" class="btn">AC</button>
    <button @click="sign" class="btn">+/-</button>
    <button @click="percent" class="btn">%</button>
    <button @click="divide" class="btn operator">÷</button>
    <button @click="append('7')" class="btn">7</button>
    <button @click="append('8')" class="btn">8</button>
    <button @click="append('9')" class="btn">9</button>
    <button @click="times" class="btn operator">×</button>
    <button @click="append('4')" class="btn">4</button>
    <button @click="append('5')" class="btn">5</button>
    <button @click="append('6')" class="btn">6</button>
    <button @click="minus" class="btn operator">-</button>
    <button @click="append('1')" class="btn">1</button>
    <button @click="append('2')" class="btn">2</button>
    <button @click="append('3')" class="btn">3</button>
    <button @click="add" class="btn operator">+</button>
    <button @click="append('0')" class="btn zero">0</button>
    <button @click="dot" class="btn">.</button>
    <button @click="equal" class="btn operator">=</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if(this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => b * a;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => b + a;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previous))}`;
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator{
    width: 330px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    font-size: 40px;
    border-radius: 10px;
    overflow: hidden;
    border: 1px solid #999;
  }

  .display{
    display: flex;
    height: 80px;
    grid-column: 1/5;
    background-color: #333;
    color: white;
    justify-content: flex-end;
  }

  .result {
    align-self: flex-end;
    font-size: 50px;
    margin-right: 20px;
  }

  .zero{
    grid-column: 1/3;
    background-color: rgb(37, 214, 96) !important;
  }

  .zero:hover {
    background-color: rgb(28, 167, 74) !important;
  }

  .btn{
    font-size: 26px;
    background-color: #f2f2f2;
    border: none;
  }

.btn:hover {
  background-color: #999;
  color: white;
}

  .operator{
    background-color: orange;
    color: white;
  }

  .operator:hover {
    background-color: darkgoldenrod;
  }
</style>
