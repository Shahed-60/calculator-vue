<template>
  <div
    class="p-3"
    style="max-width: 400px; margin: 50px auto; background: #234"
  >
    <!-- claculator resultaat -->
    <div
      class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-dark"
      style="text-align: right"
    >
      <!-- als de er geen waarde leeg staat geeft die 0 treug -->
      {{ calculatorValue || 0 }}
    </div>
    <!-- calculator knoppen -->
    <div class="row no-gutters">
      <!-- key moet uniek zijn en moet string of numeriek  -->
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div
          class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{
            'bg-vue-green': ['C', '*', '/', '-', '+', '%', '='].includes(n),
          }"
          @click="action(n)"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "MyCalculator",
  props: {
    msg: String,
  },

  data() {
    return {
      calculatorValue: "",
      calculatorElements: [
        "C",
        "*",
        "/",
        "-",
        "7",
        "8",
        "9",
        "+",
        "4",
        "5",
        "6",
        "%",
        "1",
        "2",
        "3",
        "=",
        "0",
        ".",
      ],
      operator: null,
      previousCalculatorValue: "",
    };
  },
  methods: {
    // waarde toevoegen aan de calculator
    action(n) {
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n + "";
      }
      // waarde verwijderen
      if (n === "C") {
        this.calculatorValue = "";
      }
      // precentage berekenen
      if (n === "%") {
        this.calculatorValue = this.calculatorValue / 100 + "";
      }
      if (["*", "/", "-", "+"].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";
      }
      if (n === "=") {
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = "";
        this.operator = null;
      }
    },
  },
};
</script>

<style scoped>
.bg-vue-dark {
  background: #31475e;
}
.hover-class:hover {
  cursor: pointer;
  background: #3d5875;
}
.bg-vue-green {
  background: #3fb984;
}
</style>
