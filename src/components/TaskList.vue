<template> 

    <div class="task-list-container">
        <h2>Lista de Tarefas</h2>

        <div class="controls">
            <button 
                :class="bttnAddClass"
                @click="handlerShowForm">
                {{ bttnAddTask }}
            </button>

            <button 
                class="bttn-toggle-all">
                Marcar Todas
            </button>

            <button 
                class="bttn-clear">
                Limpar Concluídas
            </button>
        </div>

        <div 
            v-if="showForm"
            class="add-task-input"
        > <!-- formulário-->

        <!--Todas as vezes que eu digitar nesse input, automaticamente o que for digitado será preenchido nessa variavel (newTaskTitle) -->
            <input 
                v-model="newTaskTitle"
                type="text"
                placeholder="Digite o titulo da tarefa"
                class="task-input"
            />

            <button 
                class="bttn-add"
                @click="addTask">
                    Adicionar
            </button>

        </div>

        <div class="tasks-container">

            <div class="pending-tasks">
                <h3>Tarefas Pendentes</h3>

                <p v-if="pendingTasks.length === 0">
                Nenhuma tarefa pendente.</p>

                <div v-else>  
                <TaskItem 
                    v-for="task in pendingTasks"
                    :key="task.id"
                    :task="task"
                    @toggle-done="toggleTaskDone"
                    @remove-task="removeTask"
                />
                </div>
            </div>

            <div class="completed-tasks">
                <h3>Tarefas Concluídas</h3>

                <p v-if="completedTasks.length === 0">
                    Nenhuma tarefa concluída.
                </p>
                
                <div v-else>
                <TaskItem 
                    v-for="task in completedTasks"
                    :key="task.id"
                    :task="task"
                    @toggle-done="toggleTaskDone"
                    @remove-task="removeTask"
                />
                </div>
            </div>

            <div>
                <h3>Resumo</h3>
                <p v-if="tasks.length === 0">
                    Você ainda não possui tarefas.
                </p>

                <p v-else-if="pendingTasks.length > 0 && completedTasks.length === 0">
                    Você tem {{ pendingTasks.length }} tarefas pendentes.
                </p>

                <p v-else-if="completedTasks.length > 0 && pendingTasks.length === 0">
                    Todas as tarefas concluídas.
                </p>

                <p v-else>
                    Você tem {{ pendingTasks.length }} pendente(s) e {{ completedTasks.length }} concluída(s)!
                </p>

            </div>

            <div class="watch-output">
                <h3>Saída do Watch ( Console )</h3>
                <div class="log-container">
                    {{ watchLogs }}
                </div>
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
    },
    data() {
        // simulando as tasks recebendo de uma API
        return {
            tasks: [
                { id: 1234, title: 'Tarefa 1' ,done: false },
                {id: 456, title: 'Tarefa 2' ,done: true }
            ],
            watchLogs: [],
            newTaskTitle: '',
            showForm: false // falso para mostrar o fomrulário
        }
    },
    methods: { // cria funções comuns
        removeTask(taskId) {
            this.tasks = this.tasks.filter(task => task.id != taskId)
            // atualiza a lista tasks e dessa lista retorna todo mundo, onde o task.id é diferente do que ele está recebendo. Se recebe 1234, retorna 456.
        },
        toggleTaskDone(taskId) {
            const task = this.tasks.find(t => t.id === taskId);
            if (task) {
                task.done = !task.done;
            }
        },
        logWatch(message) {
            this.watchLogs.unshift(`[${new Date().toLocaleDateString()}] ${message}`)
        },
        addTask() {
            // se o valor do newTaskTitle, sem os espaços, for vazio significa que o usuário não digitou nada, então não quero que execute a ação
            // .trim() => remove os espaços

            if (this.newTaskTitle.trim() === '') return

            this.tasks.push({
                id: Date.now(),
                title: this.newTaskTitle.trim(),
                done: false
            })

            this.newTaskTitle = ''
            this.showForm = false
        },
        handlerShowForm() {
            this.showForm = !this.showForm
        }


    },
    watch: { //  Observa a mudança de uma var específica 
            // -- escuta a lista de tarefas (tasks) 
        tasks: {
            handler(newVal, oldVal) {
                const message = `Lista de Tasks mudou! Itens: ${newVal.length}`
                this.logWatch(message)
                if (oldVal) {
                    const modified = newVal.filter(n => {
                        const oldTask = oldVal.find(o => o.id === n.id);
                        return oldTask && JSON.stringify(n) !== JSON.stringify(oldTask); // operação ternária
                    })
                    if (modified.length > 0) {
                        const modifyMsg = `Tarefas modificadas: ${modified.map(t => t.id).join(', ')}`
                        this.logWatch(modifyMsg)
                    }
                }
            },
            deep: true,
            immediate: true
        }
    },
    computed: { // cria valores salvos na memória com base em outros dados
        completedTasks() {
            return this.tasks.filter(task => task.done) // done true
        },
        pendingTasks(){
            return this.tasks.filter(task => !task.done) // done false
        },
        bttnAddTask() {
            return this.showForm
                ? 'Fechar'
                : 'Adicionar nova tarefa'
        },
        bttnAddClass() {
            return this.showForm
                ? 'bttn-clear'
                : 'bttn-add'
        }
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
    color:rgb(35, 36, 32);
    margin-bottom: 20px;
    padding-bottom: 10px;
    border-bottom: 2px solid rgb(47, 45, 51);
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
    background-color: rgba(98, 201, 38, 0.808);
    color: rgb(255, 255, 255);
}

.bttn-add:hover {
    background-color: rgba(90, 238, 70, 0.945);
    transform: translateY(-2px);
}

.bttn-toggle-all {
    background-color:  rgb(104, 190, 216);
    color: #fefeff;
}

.bttn-toggle-all:hover {
    background-color: rgb(116, 213, 243);
    transform: translateY(-2px);
}

.bttn-clear {
    background-color: rgb(252, 130, 126);
    color: #faf9fd;
}

.bttn-clear:hover {
    background-color:rgb(250, 139, 139);
    transform: translateY(-2px);
}

.tasks-container {
    display: grid;
    gap: 15px;
    margin-bottom: 30px;
}

.pending-tasks, .completed-tasks {
    padding: 20px;
    border-radius: 8px;
}

.pending-tasks {
    background-color: rgb(241, 239, 239);
    border:  2px solid #eeeded;
}

.completed-tasks {
    background-color: rgb(229, 253, 215);
    border:  2px solid #daf5bc;
}

.pending-tasks h3, .completed-tasks h3 {
    margin-top: 0;
    margin-bottom: 15px;
    color: rgb(34, 34, 33);
    text-align: center;
}

.watch-output {
    background-color: #2c3e50;
    color: white;
    padding: 15px;
    border-radius: 6px;
}

.log-container {
    max-height: 200px;
    overflow-y: auto;
    background-color: #1a242f;
    padding: 10px;
    border-radius: 4px;
    margin-top: 10px;
    font-family: monospace;
}

.add-task-input {
    display: flex;
    gap: 10px;
    justify-content: center;
    margin-bottom: 20px;
}

.task-input {
    padding: 10px;
    border: 1px solid #f5f1f1;
    width: 300px;
}

</style>