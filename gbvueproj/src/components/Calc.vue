<template>
  <div>
    <h1>{{ title }}</h1>
    <input v-model.number="operand1" />
    <input v-model.number="operand2" />
    <div>
      <button @click="calculate($event)">+</button>
      <button @click="calculate($event)">-</button>
      <button @click="calculate($event)">*</button>
      <button @click="calculate($event)">/</button>
      <button @click="calculate($event)">^</button>
      <button @click="calculate($event)">f</button>
    </div>
    <p>{{ result }}</p>
  </div>
</template>

<script>
export default {
  name: "Calc",
  data: () => ({
    operand1: 0,
    operand2: 0,
    result: 0,
  }),
  props: {
    title: String,
  },
  methods: {
    calculate(operation) {
      //   console.log(operation.target.outerText);
      switch (operation.target.outerText) {
        case "+":
          this.result = this.operand1 + this.operand2;
          break;
        case "-":
          this.result = this.operand1 - this.operand2;
          break;
        case "*":
          this.result = this.operand1 * this.operand2;
          break;
        case "/":
          this.result = this.operand1 / this.operand2;
          break;
        case "^":
          this.result = Math.pow(this.operand1, this.operand2);
          break;
        case "f":
          this.result = Math.floor(this.operand1 / this.operand2);
          break;
      }
    },
  },
};
</script>