<template>
  <div class="home">
    <Calculator :history="history"></Calculator>
  </div>
</template>

<script>
import Calculator from '../components/Calculator.vue'

export default {
  name: 'CalculatorView',

  components: {
    Calculator
  },
  computed: {
    history() {
      return this.$root.$data.history;
    }
  }
}
</script>