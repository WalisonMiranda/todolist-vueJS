<template>
    <div class="todo-item">
        <h3>To-Do item</h3>
        <div class="new-todo">
            <InputText 
                class="input" 
                v-model="description"
                placeholder="Descrição da tarefa"
            />
        </div>
        <div class="div-botoes">
            <Button @click="saveTodo">Salvar</Button>
            <Button class="p-button-secondary" @click="cancel">Cancelar</Button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            description: ""
        }
    },
    props: {
        todo: Object
    },
    created() {
        if(this.todo) {
            this.description = this.todo.description;
        }

    },
    methods: {
        cancel() {
            this.$emit("cancel");
        },
        saveTodo() {
            this.$emit("saveTodo", { ...this.todo, description: this.description });
        }
    }
}
</script>

<style scoped>
    .todo-item {
        margin: 4.5rem 2rem auto 2rem;
        background-color: #673ab7;
        padding: 2rem 1rem;
        border-radius: 4px;
    }

    .todo-item h3 {
        margin-left: 2rem;
    }

    .new-todo {
        padding: 1rem;
    }

    .input {
        flex-grow: 1;

        color: #482880;
    }

    .div-botoes {
        margin: 1rem;
    }

    .div-botoes Button {
        margin-left: 1rem;
    }

</style>