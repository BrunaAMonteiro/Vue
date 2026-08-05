<template>

    <div class="task-item">
        <span class="task-id"># 123</span>
        <span class="task-status">Concluída</span>
        <button class="bttn-toggle">
            Concluir
        </button>
        <button class="bttn-remove">
            Remover
        </button>
    </div>

</template>

<script>

export default {
    name: 'TaskItem'
}
</script>

<style>

.task-item {
    display: flex;
    align-items: center;
    padding: 10px;
    margin-bottom: 8px;
    border-radius: 5px;
    background-color: rgb(34, 21, 21);
    border: 1px solid gray;
    transition: all 0.3;
}

.task-id {
    font-weight: bold;
    margin-right: 10px;
    color: palevioletred;
}

.task-status {
    flex-grow: 1;
}

.bttn-toggle {
    background-color: aqua;
    color: rgb(29, 90, 85);
    margin-right: 5px;
}

.bttn-toggle:hover {
    background-color: rgb(143, 210, 236);
}

.bttn-remove {
    background-color: rgb(0, 132, 255);
    color: rgb(30, 35, 78);
}

.bttn-remove:hover {
    background-color: rgb(92, 174, 252);
}

</style>

<!-- muda as cores e ve se ta certo mesmo, pq ta faltando um bttn -->