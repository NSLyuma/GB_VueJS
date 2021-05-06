<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p @click="sum">{{ sumAB }}</p>
    <!--при клике на заголовок в консоль выводится сумма a и b-->
    <button id="ev" @click="event($event)">{{ eventFunc }}</button>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: () => ({
    sumAB: "Сумма a и b",
    eventFunc: "Event",
    a: 2,
    b: 4,
    c: 0,
  }),
  props: {
    msg: String,
    myBool: Boolean,
  },
  methods: {
    sum() {
      console.log(this.a + this.b);
    },
    event(e) {
      console.log(e);
    },
  },
  computed: {},
  watch: {
    message() {},
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
