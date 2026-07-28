<template>

    <div class="bttns">
        <MyButton title="soma"
        @update="$emit('change-count', 'increment', 1)"
        />

        <MyButton title="subtração"
        @update="$emit('change-count', 'decrement', 1)"
        />
        <MyButton tittle="resetar"
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
    }
}

</script>

<style>

.bttns {
    display: flex;
    gap: 10px;
}

</style>