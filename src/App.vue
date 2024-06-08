<template>
  <div id="app">
    <h1>DYLAN</h1>
    <input v-model="input" @keyup.enter="calculate" readonly/>
    <p class= "result">  {{ result }}</p>
    <section class="function">
      <div class="row justify-content-around g-5 pb-3">
          <button class="col-auto mx-2" @click="sqrt()">sqrt</button>
          <button class="col-auto mx-2" @click="exp()">exp</button>
          <button class="col-auto mx-2" @click="ln()">ln</button>
          <button class="col-auto mx-2" @click="log()">log</button>
          <button class="col-auto mx-2" @click="factoriel()">n!</button>
        </div>
    </section>
    <section class="basics">
        <div class="buttons-container">
          <!-- Boutons numériques -->
          <button class="numbuttons" v-for="button in numericButtons" :key="'num' + button" @click="appendToInput(button)">
            {{ button }}
          </button>
          <button @click="appendToInput('.')">,</button>
          <button class="btn btn-primary" @click="calculate">=</button>
        </div>
        <div class="buttons-container2">
          <button @click="clear">C</button>
          <button class="btn btn-danger" @click="backspace">⌫</button>
          <!-- Boutons opérateurs -->
          <button v-for="button in operatorButtons" :key="'op' + button" @click="appendToInput(button)">
            {{ button }}
          </button>
        </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: '',
      result: '',
      numericButtons: [7, 8, 9, 4, 5, 6, 1, 2, 3, 0],
      operatorButtons: [ '-', '+', '*', '/', '(', ')']
    };
  },
  methods: {
    appendToInput(button) {
      this.input += button;
    },
    calculate() {
      try {
        this.result = eval(this.input);
      } catch (e) {
        this.result = 'Erreur!';
      }
    },
    clear() {
      this.input = '';
      this.result = '';
    },
    backspace() {
      this.input = this.input.slice(0, -1);
    },
    sqrt() {
      this.result = Math.sqrt(eval(this.input)).toString();
    },
    exp(){
      this.result = Math.exp(eval(this.input)).toString();
    },
    ln(){
      this.result = Math.log(eval(this.input)).toString();
    },
    log(){
      this.result = Math.log10(eval(this.input)).toString();
    },
    factoriel(){
      const num = parseInt(this.input);
      if (isNaN(num) || num < 0) {
        this.result = 'Erreur!';
      } else {
        this.result = this.factorielCalc(num).toString();
      }
    },
    factorielCalc(n){
      if(n === 0 || n ===1){
        return 1;
      }
      return n * this.factorielCalc(n-1);
    }
  }
}
</script>

<style src="@/assets/bootstrap.min.css">
</style>

<style lang="scss">
template{
  background: white;
}
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: Arial, sans-serif;
  border: 6px solid rgb(26, 25, 25);
  background: rgb(26, 25, 25);
  border-radius: 10px;
  padding: 10px 0;
  margin-top: 50px;
}

input {
  width: 400px;
  height: 90px;
  font-size: 30px;
  text-align: right;
  font-family: monospace;
  margin-bottom: 10px;
  color:  white;
  background: transparent;
  border: none;
  border-radius: 5px;
  overflow-x: nowrap;
}

p.result{
  z-index: 1;
  width: 400px;
  text-align: right;
  color: #777;
  font-family: monospace;
  font-size: 40px;
  font-weight: bold;
  margin-top: -20px;
}

section.basics{
  display: flex;
  flex: wrap;
}

.buttons-container {
  display: grid;
  grid-template-columns: repeat(3, 75px);
  grid-gap: 10px;
}

.buttons-container2 {
  margin: 0 0 0 20px;
  display: grid;
  grid-template-columns: repeat(2, 75px);
  grid-gap: 10px;
}

button {
  width: 75px;
  height: 60px;
  font-size: 20px;
  background-color: #333;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #555;
}

button:active {
  background-color: #777;
}
</style>