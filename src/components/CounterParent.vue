<template>
    <CounterChild 
    v-bind:count="myCount"
    v-on:update_hogehoge="handleUpdate" />
</template>

<script>
import CounterChild from './CounterChild.vue'
export default {
    components: { CounterChild },
    data() { return {myCount: 0}},
    methods: {
        handleUpdate(newCount) {
            this.myCount = newCount
        }
    },
}
</script>