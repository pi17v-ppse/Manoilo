<template>
  <div class="container">
    <div class="calc">
      <div class="text">
        3.14
      </div>

      <div class="buttons">
        <button class="calc__button">C</button>
        <button class="calc__button">Back</button>
        <button class="calc__button">/</button>
        <button class="calc__button">*</button>
        <button class="calc__button">7</button>
        <button class="calc__button">8</button>
        <button class="calc__button">9</button>
        <button class="calc__button">-</button>
        <button class="calc__button">4</button>
        <button class="calc__button">6</button>
        <button class="calc__button">7</button>
        <button class="calc__button plus__button">+</button>
        <button class="calc__button">1</button>
        <button class="calc__button">2</button>
        <button class="calc__button">3</button>
        <button class="calc__button equals__button">=</button>
        <button class="calc__button">0</button>
        <button class="calc__button">.</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld'
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
  text-align: right;
}

.text{
  width: 100%;
  border: 1px solid black;
  border-radius: 1px;
  margin-bottom: 12px;
  padding: 10px;
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

.plus__button{
  grid-row-start: 5;
  grid-column-start: 1;
  grid-column-end: 3;
}
</style>
