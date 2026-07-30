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

<style>

.task-item {
    display: flex;
    align-items: center;
    padding: 10px;
    margin-bottom: 8px;
    border-radius: 5px;
    background-color: white;
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
    color: white;
    margin-right: 5px;
}

.bttn-toggle:hover {
    background-color: rgb(143, 210, 236);
}

.bttn-remove {
    background-color: rgb(0, 132, 255);
    color: white;
}

.bttn-remove:hover {
    background-color: rgb(92, 174, 252);
}

</style>