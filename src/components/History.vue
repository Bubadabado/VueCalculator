<template>
    <div class="history">
        <div v-if="!empty">
            <button class="button" @click="clearHistory">Clear History</button>
            <div v-for="operation in getHistory" :key="operation.id">
                <p>{{operation}}</p>
            </div>
        </div>
        <div v-else>
            <p>The history is currently empty.</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "HistoryComp",
    props: {
        history: Array
    },
    computed: {
        getHistory() {
            return this.$root.$data.history;
        },
        empty() {
            return this.$root.$data.history.length == 0;
        }
    },
    methods: {
        clearHistory() {
            this.$root.$data.history = [];
        }
    }
}
</script>

<style scoped>
.button {
    background-color: rgb(66, 49, 114);
    color: white;
    padding: 10px;
    border: none;
    border-radius: 6px;
}
</style>