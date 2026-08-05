<template> 

    <div class="task-list-container">
        <h2>Lista de Tarefas</h2>

        <div class="controls">
            <button clas="bttn-add">Adicionar nova tarefa</button>
            <button class="bttn-clear">
                Limpar Concluídas
            </button>
        </div>

        <div class="tasks-container">

            <div class="pending-tasks">
                <h3>Tarefas Pendentes</h3>
                <TaskItem />
            </div>

            <div class="completed-tasks">
                <h3>Tarefas Concluídas</h3>
                <TaskItem />
            </div>

        </div>

        <span>Aqui virá o componente dos contadores</span>

    </div>

</template>

<script>

import TaskItem from './TaskItem.vue'

export default {

    name: 'TaskList',
    components: {
        TaskItem
    }
    
}

</script>

<style>

.task-list-container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 20px;
}

h2 {
    color:blueviolet;
    margin-bottom: 20px;
    padding-bottom: 10px;
    border-bottom: 2px solid rgb(82, 47, 163);
    text-align: center;
}

.controls {
    display: flex;
    gap: 10px;
    margin-bottom: 30px;
    flex-wrap: wrap;
    justify-content: center;
}

button {
    padding: 10px 20px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-weight: bold;
    transition: all 0.3;
    font-size: 14px;
}

.bttn-add {
    background-color: plum;
    color: rgb(81, 66, 145);
}

.bttn-add:hover {
    background-color: rgb(231, 116, 247);
    transform: translateY(-2px);
}

.bttn-toggle-all {
    background-color: plum;
    color: rgb(182, 120, 211);
}

.bttn-toggle-all:hover {
    background-color: rgb(231, 116, 247);
    transform: translateY(-2px);
}

.bttn-clear {
    background-color: plum;
    color: #2719aa;
}

.bttn-clear:hover {
    background-color: rgb(231, 116, 247);
    transform: translateY(-2px);
}

.task-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 30px;
    margin-bottom: 30px;
}

.pending-tasks, .completed-tasks {
    padding: 20px;
    border-radius: 8px;
}

.pending-tasks {
    background-color: rgb(212, 76, 76);
    border:  2px solid #fd2323;
}

.completed-tasks {
    background-color: rgb(171, 238, 132);
    border: 2px solid #43f30e;
}

.pending-tasks h3, .completed-tasks h3 {
    margin-top: 0;
    margin-bottom: 15px;
    color: rgb(37, 36, 10);
    text-align: center;
}

</style>