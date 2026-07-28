<template>
    <button @click="$emit('update')">
        {{ title }}
    </button>
</template>

<script>

export default {
    name: 'MyButton',
    props: {
        title: {
            type: String,
            default: '+1'
        },

    }
}

</script>

<style>
button {
    padding: 10px 20px;
    background-color: palevioletred;
    color: aliceblue;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: rgb(253, 173, 187);
}
</style>