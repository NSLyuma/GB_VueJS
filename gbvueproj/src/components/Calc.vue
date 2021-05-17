<template>
  <div>
    <h1>{{ title }}</h1>
    <input v-model.number="operand1" />
    <input v-model.number="operand2" />
    <div>
      <button v-for="op in operations" :key="op" @click="calculate(op)">
        {{ op }}
      </button>
      <!-- эти 6 строк можно заменить одной, которая сверху
      <button @click="calculate('+')">+</button>
      <button @click="calculate('-')">-</button>
      <button @click="calculate('*')">*</button>
      <button @click="calculate('/')">/</button>
      <button @click="calculate('^')">^</button>
      <button @click="calculate('f')">f</button> -->
    </div>
    <p>{{ result }}</p>

    <div class="error" v-if="error">
      <!-- если выполняется условие (error не пустой), то покажи этот блок -->
      <!-- v-if полностью убирает блок из вёрстки, v-show скрывает с помощью display: none -->
      {{ error }}
    </div>

    <!-- пример работы с if
    <div v-if="result < 0">Получилось отрицательное число</div>
    <div v-else-if="result <= 1000">
      Результат находится в промежутке от 0 до 1000
    </div>
    <div v-else>Результат слишком большой (>1000)</div> -->

    <div>
      <label>
        <input type="checkbox" id="checkbox" v-model="checked" />
        Отобразить экранную клавиатуру
      </label>
    </div>

    <div v-if="checked">
      <button v-for="(item, index) in numbers" v-bind:key="index">
        {{ item }}
      </button>

      <div>
        <input type="radio" name="operand" id="first" v-model="first" checked />
        <label for="first">Операнд 1</label>
        <input type="radio" name="operand" id="second" v-model="second" />
        <label for="second">Операнд 2</label>
      </div>
    </div>
    <br />
    <br />
    <br />

    <div>
      <!-- <input type="radio" id="one" value="Один" v-model="picked" />
      <label for="one">Один</label>
      <br />
      <input type="radio" id="two" value="Два" v-model="picked" />
      <label for="two">Два</label>
      <br />
      <span>Выбрано: {{ picked }}</span> -->
    </div>
  </div>
</template>

<script>
export default {
  name: "Calc",
  data: () => ({
    operations: ["+", "-", "*", "/", "^", "f"],
    operand1: 0,
    operand2: 0,
    result: 0,
    error: "",
    numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    checked: true,
    first: true,
    second: false,
  }),
  props: {
    title: String,
  },
  methods: {
    calculate(operation) {
      //   console.log(operation.target.outerText);
      //   switch (operation) {
      //     case "+":
      //       this.result = this.operand1 + this.operand2;
      //       break;
      //     case "-":
      //       this.result = this.operand1 - this.operand2;
      //       break;
      //     case "*":
      //       this.result = this.operand1 * this.operand2;
      //       break;
      //     case "/":
      //       this.result = this.operand1 / this.operand2;
      //       break;
      //     case "^":
      //       this.result = Math.pow(this.operand1, this.operand2);
      //       break;
      //     case "f":
      //       this.result = Math.floor(this.operand1 / this.operand2);
      //       break;
      //   }
      const { operand1, operand2 } = this;

      if (operation === "/" && operand2 === 0) {
        this.error = "Division by zero!";
        return;
      }

      let calc = {
        "+": (op1, op2) => {
          return op1 + op2;
        },
        "-": (op1, op2) => {
          return op1 - op2;
        },
        "*": (op1, op2) => {
          return op1 * op2;
        },
        "/": (op1, op2) => {
          return op1 / op2;
        },
        "^": (op1, op2) => {
          return Math.pow(op1, op2);
        },
        f: (op1, op2) => {
          return Math.floor(op1 / op2);
        },
        operation: (op1, op2, operator) => {
          return calc[operator](op1, op2);
        },
      };
      this.result = calc.operation(operand1, operand2, operation);
    },
  },
  computed: {
    //не принимают параметры и обязательно возвращают какое-то значение
  },
};
</script>

<style scoped lang="scss">
.error {
  padding: 20px;
  border: 1px solid red;
}
</style>