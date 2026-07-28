<template>

    <div id="box">
        {{ name }} {{ age }}
        <span :class="['status', status]">{{ status }}</span>
        <!-- procura no array se é active ou inactive e printa;
        SPAN => agrupar pedaços de texto, mudar a cor de uma palavra e aplicar estilos sem quebrar a linha -->
    </div>

</template>

<script>

export default {
    name: 'MyBox',
    props: {
        // propriedade do MyBox ==> text uqe tem o tipo String e valor default 'N/A'
        name: {
            type: String,
            default: 'N/A'
        },
        age: {
            type: Number,
            required: true,
        },
        status: {
            type: String,
            validator: value => ['active', 'inactive'].includes(value),
            default: 'active'
        }
    }
}

</script>

<style>
.active {
    background-color: rgb(163, 248, 163);
}

.inactive {
    background-color: rgb(185, 183, 183);
}

#box {
    min-width: 50px;
    min-height: 50px;
    background-color: rgb(225, 192, 255);
    align-items: center;
    justify-content: center;
    display: flex;
}
</style>