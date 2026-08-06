<template>

    <div class="task-item">

        <span class="task-id"># {{ task?.id }}</span> <!-- propriedade-->
        <span class="task-status">{{ statusText }}</span> <!-- propriedade-->

        <button 
        class="bttn-toggle" 
        @click="toggleDone">

            {{ bttnToggleText }}
        </button>

        <button 
        class="bttn-remove" 
        @click="removeTask">

            Remover
        </button>
    </div>

</template>

<script>

export default {
    name: 'TaskItem',
    props: {
        task: { // dois atributos == id e done(concluida ou nao)
            type: Object,
            required: true
        }
    },

    methods: {
        toggleDone() {
            this.$emit('toggle-done', this.task?.id) // precisa passar o id da task
        },
        removeTask() {
            this.$emit('remove-task', this.task.id) // precisa passar o id da task
        }
    },

    computed: {
        bttnToggleText() {
            return this.task?.done
                ? 'Desfazer'
                : 'Concluir'
        },
        statusText() {
            return this.task?.done
                ? 'Concluída'
                : 'Pendente'
        }
    },
}
</script>

<style>

.task-item {
    display: flex;
    align-items: center;
    padding: 10px;
    margin-bottom: 8px;
    border-radius: 5px;
    background-color: rgb(255, 255, 255);
    border: 1px solid rgb(249, 247, 255);
    transition: all 0.3;
}

.task-id {
    font-weight: bold;
    margin-right: 10px;
    color: rgb(53, 49, 50);
}

.task-status {
    flex-grow: 1;
}

.bttn-toggle {
    background-color: rgb(205, 250, 164);
    color: rgb(47, 105, 45);
    margin-right: 5px;
}

.bttn-toggle:hover {
    background-color: rgb(169, 252, 143);
}

.bttn-remove {
    background-color: rgb(250, 146, 139);
    color: rgb(109, 18, 18);
}

.bttn-remove:hover {
    background-color: rgb(248, 118, 109);
}

</style>

<!-- muda as cores e ve se ta certo mesmo, pq ta faltando um bttn -->