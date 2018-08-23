<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div> 
    <div @click="clear" class="btn">AC</div>
    <div class="btn">+/-</div>
    <div class="btn">%</div>
    <div @click="divider" class="btn btn-orange">/</div>
    <div @click="number(7)" class="btn">7</div>
    <div @click="number(8)" class="btn">8</div>
    <div @click="number(9)" class="btn">9</div>
    <div @click="multiple" class="btn btn-orange">*</div>
    <div @click="number(4)" class="btn">4</div>
    <div @click="number(5)" class="btn">5</div>
    <div @click="number(6)" class="btn">6</div>
    <div @click="minus" class="btn btn-orange">-</div>
    <div @click="number(1)" class="btn">1</div>
    <div @click="number(2)" class="btn">2</div>
    <div @click="number(3)" class="btn">3</div>
    <div @click="pluse" class="btn btn-orange">+</div>
    <div @click="number(0)" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="result" class="btn btn-orange">=</div> 
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      previous: null,
      current: '',
      operator: null
    }
  },
  methods: {
    clear() {
      this.current = '';
      this.operator = null;
    },
    number(value) {
      if(this.operator instanceof Function) {
        this.current = value;
      } else {
        this.current = this.current.concat(value);
      }
    },
    divider() {
      this.operator = (a, b) => { return a / b }
      this.setPrevious();
    },
    multiple() {
      this.operator = (a, b) => { return a * b }
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => { return a - b }
      this.setPrevious();
    },
    pluse() {
      this.operator = (a, b) => { return a + b }
      this.setPrevious();
    },
    dot() {
      if(this.current.indexOf('.') === -1) {
        this.current = this.current.concat('.');
      }
    },
    result() {
      if(this.operator instanceof Function) {
        this.current = this.operator(parseFloat(this.previous), parseFloat(this.current));
      }
    },
    setPrevious() {
      this.previous = this.current;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  color: white;
  font-size: 40px;
  border: solid 1px gray;
  margin: 0 auto;
  width: 400px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1 / 5;
  background-color: rgb(52, 63, 63);
}

.btn {
  cursor: pointer;
  border: solid 1px rgb(206, 206, 206);
  background-color: rgb(80, 80, 80);
}

.btn:hover {
  background-color: rgb(231, 231, 231);
  color: black;
}

.btn-orange {
  background-color: rgb(255, 177, 32);
}

.zero {
  grid-column: 1 / 3;
}

</style>
