<template>
  <div class="container">
    <div class="calc">
      <input v-model="result" class="text" placeholder="0" readonly>

      <div class="buttons">
        <button @click="clear()" class="calc__button">C</button>
        <button @click="backspace()" class="calc__button">Back</button>
        <button @click="set_operation('/')" class="calc__button">/</button>
        <button @click="set_operation('*')" class="calc__button">*</button>
        <button @click="insert('7')" class="calc__button">7</button>
        <button @click="insert('8')" class="calc__button">8</button>
        <button @click="insert('9')" class="calc__button">9</button>
        <button @click="set_operation('-')" class="calc__button">-</button>
        <button @click="insert('4')" class="calc__button">4</button>
        <button @click="insert('5')" class="calc__button">5</button>
        <button @click="insert('6')" class="calc__button">6</button>
        <button @click="set_operation('+')" class="calc__button">+</button>
        <button @click="insert('1')" class="calc__button">1</button>
        <button @click="insert('2')" class="calc__button">2</button>
        <button @click="insert('3')" class="calc__button">3</button>
        <button @click="calc()" class="calc__button equals__button">=</button>
        <button @click="negate()" class="calc__button">+/-</button>
        <button @click="insert('0')" class="calc__button">0</button>
        <button @click="insert('.')" class="calc__button">.</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return {
      result: '',
      operation: null,
      operator_a: null,
      operator_b: null
    }
  },
  methods: {
    set_operation(operation){
      this.operation = operation;
      this.operator_a = this.result;
      this.result = '';
    },
    insert(char_to_insert){
      switch (char_to_insert){
        case '.':
          if (!this.result.includes('.')){
            if (this.result == '')
              char_to_insert = '0' + char_to_insert;
            this.result += char_to_insert;
          }
          break;
        case '0':
          if (this.result != '0')
            this.result += char_to_insert;
          break;
        default:
          if (this.result == '0')
            this.result = char_to_insert;
          else
            this.result += char_to_insert;
          break;
      }
    },
    clear(){
      this.result = '';
    },
    backspace(){
      this.result = this.result.slice(0, -1);
    },
    calc(){
      if (this.result != ''){
        this.operator_b = this.result;
        switch (this.operation){
          case '+':
            this.result = (parseFloat(this.operator_a) + parseFloat(this.operator_b)).toString();
            break;
          case '-':
            this.result = (parseFloat(this.operator_a) - parseFloat(this.operator_b)).toString();
            break;
          case '*':
            this.result = (parseFloat(this.operator_a) * parseFloat(this.operator_b)).toString();
            break;
          case '/':
            this.result = (parseFloat(this.operator_a) / parseFloat(this.operator_b)).toString();
            break;
        }
      }
    },
    negate(){
      this.result = (parseFloat(this.result) * -1).toString();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*{
  box-sizing: border-box;
}

.container{
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  background: linear-gradient(to right, #e91e63, #3f51b5);
}

.calc{
  width: 231px;
  margin: 0 auto;
  padding: 10px;
}

.text{
  width: 100%;
  border: none;
  text-align: right;
  border-radius: 1px;
  margin-bottom: 12px;
  padding: 10px;
  font-size: 14pt;
  background-color: white;
}

.buttons{
  display: grid;
	grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 48px;
  grid-gap: 6px;
}

.calc__button{
  font-size: 12pt;
  color: white;
  background-color: #607d8b;
  border: none;
}

.calc__button:hover{
  cursor: pointer;
}

.equals__button{
  grid-column-start: 4;
  grid-row-start: 4;
  grid-row-end: 6;
}
</style>
