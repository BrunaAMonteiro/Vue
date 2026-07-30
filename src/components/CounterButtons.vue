<template>

    
    <div class="bttns">

        <h2> Valor atual de count: {{ countValue }} </h2>

        <MyButton title="soma"
        @update="$emit('change-count', 'increment', 1)"
        />

        <MyButton 
        title="subtração"
        :disabled="!canDecrement"
        @update="$emit('change-count', 'decrement', 1)"
        />

        <MyButton 
        title="resetar"
        :disabled="!canReset"
        @update="$emit('change-count', 'reset')"
        />
    </div>

</template>

<script>

    import MyButton from './MyButton.vue';

    export default {
    name: 'CounterButtons',
    emits: ['change-count'],
    components: {
        MyButton
    },
    props: {
        countValue: {
        // pra passar o valor desta prop, usamos o '-'. Separamos as palavras
            type: Number,
            required: true,
        }
    },
    computed: {
        canDecrement() {
            return this.countValue > -10
        },
        canReset() {
            return this.countValue !== 0
        }
    }
}

</script>

<style>

.bttns {
    display: flex;
    gap: 10px;
}

</style>