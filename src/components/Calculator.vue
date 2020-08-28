
<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div @click="clear()" class="btn">C</div>
    <div @click="sign()" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="times" class="btn operator">X</div>
    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append(0)" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  props: {
    msg: String
  },

  data() {
    return {
      previous: null,
      current: '123',
      operator: '',
      clickedOperator: false,

    }
  },

  methods: {
    clear() {
      this.current = '';
    },

    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1)  : `-${this.current}`;
    },

    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },

    append(number) {
      
      if(this.clickedOperator) {
        this.current = '';
        this.clickedOperator = false;
      }

      for(let i = 0; i < 1; i++) {
        this.current.charAt(i) === '0' ? this.current = '' : this.current = `${this.current}${number}`;
      }

    },
    
    dot() {
      if(this.current.indexOf('.') === -1){
        this.append('.');
      }
    },

    setPrevious() {
      this.previous = this.current;
      this.clickedOperator = true;
    },

    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },

    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },

    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },

    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },

    equal() {
      this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`;
      this.previous = null;
    }

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator {
    margin: 0 auto;
    width: 400px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px auto);
  }

  .display {
    grid-column: 1 / 5;
    background-color: black;
    color:white;
    font-size: 50px;
    padding: 20px 0;
  }

  .btn {
    padding:20px;
    cursor: pointer; 
    font-size: 30px;
    border: 1px solid black;
    background-color: #eee;
  }

  .zero {
    grid-column: 1/3;
  }

  .operator {
    background-color: orange;
    color:white;
    font-size: 30px;
  }
</style>
