<template>
    <div>
        カウント：{{ count }}
        <button v-on:click="handleClick">+1</button>
    </div>
</template>

<script>
export default({
    props: { count: { type: Number}},
    emits: ['update_hogehoge'],
    methods: {
        handleClick() {
            const newCount = this.count + 1
            this.$emit('update_hogehoge', newCount)
        }
    }
})
</script>


