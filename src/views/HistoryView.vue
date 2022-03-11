<template>
  <div class="history-page">
    <h2>Calculator Operation History</h2>
    <HistoryComp :history="getHistory"></HistoryComp>
  </div>
</template>

<script>
import HistoryComp from '../components/History.vue'

export default {
  name: 'HistoryView',

  components: {
    HistoryComp
  },
  computed: {
    getHistory() {
      return this.$root.$data.history;
    }
  }
}
</script>