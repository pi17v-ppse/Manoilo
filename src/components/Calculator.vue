<template>
  <div class="container">
    <div class="calc">
      <input v-model="result" class="text" placeholder="0" readonly>

      <div class="buttons">
        <button @click="clear()" class="calc__button">C</button>
        <button @click="backspace()" class="calc__button">Back</button>
        <button class="calc__button">/</button>
        <button class="calc__button">*</button>
        <button @click="insert('7')" class="calc__button">7</button>
        <button @click="insert('8')" class="calc__button">8</button>
        <button @click="insert('9')" class="calc__button">9</button>
        <button class="calc__button">-</button>
        <button @click="insert('4')" class="calc__button">4</button>
        <button @click="insert('5')" class="calc__button">5</button>
        <button @click="insert('6')" class="calc__button">6</button>
        <button class="calc__button">+</button>
        <button @click="insert('1')" class="calc__button">1</button>
        <button @click="insert('2')" class="calc__button">2</button>
        <button @click="insert('3')" class="calc__button">3</button>
        <button class="calc__button equals__button">=</button>
        <button @click="insert('0')" class="calc__button zero__button">0</button>
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
    insert(char_to_insert){
      if (char_to_insert == '.'){
        if (this.result.includes('.')){
          char_to_insert = '';
        }
        else if (this.result == ''){
          char_to_insert = '0' + char_to_insert;
        }
      }
      this.result += char_to_insert
    },
    clear(){
      this.result = '';
    },
    backspace(){
      this.result = this.result.slice(0, -1);
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

.zero__button{
  grid-row-start: 5;
  grid-column-start: 1;
  grid-column-end: 3;
}
</style>
