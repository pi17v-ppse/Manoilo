<template>
  <div class="container">
    <div class="calc">
      <input v-model="result" class="text" placeholder="0" readonly>

      <div class="buttons">
        <button @click="percentage()" class="calc__button">%</button>
        <button @click="full_clear()" class="calc__button">CE</button>
        <button @click="clear()" class="calc__button">C</button>
        <button @click="backspace()" class="calc__button fas fa-backspace"></button>
        <button @click="dividing()" class="calc__button">1/x</button>
        <button @click="power()" class="calc__button">pow</button>
        <button @click="square()" class="calc__button fas fa-square-root-alt"></button>
        <button @click="set_operation('/')" class="calc__button">/</button>
        <button @click="insert('7')" class="calc__button">7</button>
        <button @click="insert('8')" class="calc__button">8</button>
        <button @click="insert('9')" class="calc__button">9</button>
        <button @click="set_operation('*')" class="calc__button">*</button>
        <button @click="insert('4')" class="calc__button">4</button>
        <button @click="insert('5')" class="calc__button">5</button>
        <button @click="insert('6')" class="calc__button">6</button>
        <button @click="set_operation('-')" class="calc__button">-</button>
        <button @click="insert('1')" class="calc__button">1</button>
        <button @click="insert('2')" class="calc__button">2</button>
        <button @click="insert('3')" class="calc__button">3</button>
        <button @click="set_operation('+')" class="calc__button">+</button>
        <button @click="negate()" class="calc__button">+/-</button>
        <button @click="insert('0')" class="calc__button">0</button>
        <button @click="insert('.')" class="calc__button">.</button>
        <button @click="calc()" class="calc__button">=</button>
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
      argument_a: null,
      argument_b: null
    }
  },
  methods: {
    /**
     * Запоминает выбраный пользователем оператор и очищает поле ввода
     * @param {string} operation один из возможных операторов (+, -, *, /)
     */
    set_operation(operation){
      this.operation = operation;
      this.argument_a = this.result;
      this.result = '';
    },
    /**
     * Производит вставку необходимого символа в input.
     * Запрещает содержание двух точек.
     * Редактирует вид числа при вводе в пустое поле точки.
     * Запрещает ввод чисел начинающихся с нуля.
     * @param {string} char_to_insert вводимый символ
     */
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
    /**
     * Выполняет очистку поля input 
     */
    clear(){
      this.result = '';
    },
    /**
     * Выполняет полную очистку поля input, введенных раннее аргументов и оператора
     * @param {string} this.result - результат вычислений, текст содержащийся в input
     * @param {string} this.operation - выбранный оператор (+, -, *, /).
     * @param {string} this.argument_a - первый аргумент вводимый пользователем
     * @param {string} this.argument_b - второй аргумент вводимый пользователем
     */
    full_clear(){
      this.result = '';
      this.operation = null,
      this.argument_a = null,
      this.argument_b = null
    },
    /**
     * Выполняет удаление последнего символа из поля отображения чисел.
     * @param {string} this.result переменная связанная с полем Input и отображающая его содержимое.
     */
    backspace(){
      this.result = this.result.slice(0, -1);
    },
    /**
     * Выполняет вычисления исходя из введенных аргументов и выбранного оператора.
     * @param {string} this.result переменная в которую помещается результат и которая связана с данными в поле input.
     * Также проверяет на неравенство null переменные аргументов.
     */
    calc(){
      if (this.result != '' && this.argument_a != null){
        this.argument_b = this.result;
        switch (this.operation){
          case '+':
            this.result = (parseFloat(this.argument_a) + parseFloat(this.argument_b)).toString();
            break;
          case '-':
            this.result = (parseFloat(this.argument_a) - parseFloat(this.argument_b)).toString();
            break;
          case '*':
            this.result = (parseFloat(this.argument_a) * parseFloat(this.argument_b)).toString();
            break;
          case '/':
            this.result = (parseFloat(this.argument_a) / parseFloat(this.argument_b)).toString();
            break;
        }
      }
    },
    /**
     * Изменяет знак введенного числа на противоположный
     * Результат помещается в поле для ввода
     */
    negate(){
      if (this.result != '')
        this.result = (parseFloat(this.result) * -1).toString();
    },
    /**
     * Возводит введенное число во вторую степень
     * Результат помещается в поле для ввода
     */
    power(){
      if (this.result != '')
        this.result = (parseFloat(this.result) * parseFloat(this.result)).toString();
    },
    /**
     * Делит единицу на ввдеденное число
     * Результат помещается в поле для ввода
     */
    dividing(){
      if (this.result != '')
        this.result = (1 / parseFloat(this.result)).toString();
    },
    /**
     * Извлекает квадратный корень из введенного числа.
     * Результат помещается в поле для ввода
     */
    square(){
      if (this.result != '')
        this.result = Math.sqrt(parseFloat(this.result)).toString();
    },
    /**
     * Без использования какого либо оператора или с использованием операторов (*, /)
     * преобразует число в процентный вид,
     * в иных случаях вычисляет процент от введенного раннее аргумента.
     * Результат помещается в поле для ввода
     */
    percentage(){
      if (this.result != '')
        if (this.operation == '+' || this.operation == '-')
          this.result = (parseFloat(this.argument_a) * (parseFloat(this.result) / 100)).toString();
        else
          this.result = (parseFloat(this.result) / 100).toString();
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
  width: 286px;
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
  background-color: #6f838d;
}
</style>
