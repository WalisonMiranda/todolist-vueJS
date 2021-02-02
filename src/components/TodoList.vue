<template>
    <div class="todo-list">
        <h3>To-Do list</h3>
        <div class="todo-items" v-for="(todo, index) in todos" :key="index">
            <label class="todo-label">
                {{todo.description}}
            </label>
            <Button 
                icon="pi pi-pencil" 
                class="p-button-rounded p-button-text"
                @click="$emit('editTodo', index)"
            />
            <Button 
                icon="pi pi-trash" 
                class="p-button-rounded p-button-text"
                @click="$emit('deleteTodo', index)" 
            />
        </div>
    </div>
</template>

<script>
export default {
    props: {
        todos: Array
    }
}
</script>

<style scoped>
    .todo-list {
        margin: 1rem;
    }

    h3 {
        margin-left: 1rem;
    }

    .todo-items {
        height: 60px;
        margin: 1rem;
        display: flex;
        align-items: center;
        padding-left: 1rem;
        background-color: #673ab7;
        border-radius: 4px;
    }

    .todo-label {
        flex-grow: 1;
    }

</style>