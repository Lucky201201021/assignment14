<template>
    <div class="square" @click="onSquareClick">{{ squareValue }}</div>
</template>
 
<script>
export default {
    name: "Square",
    props: {
        squareValue: String,
        actionFill: Function,
    },
    methods: {
        onSquareClick() {
            this.$emit('actionFill');
        }
    },
    mounted() {

    }
}
</script>

<style>
</style>