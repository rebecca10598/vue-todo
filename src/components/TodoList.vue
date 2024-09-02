<template>
    <div class="todo-list">
        <h1>Vue.js To-Do List</h1>
        <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new task" />
        <ul>
            <li v-for="(todo, index) in todos" :key="index">
                <input type="checkbox" v-model="todo.done" />
                <span :class="{ done: todo.done }">{{ todo.text }}</span>
                <button @click="removeTodo(index)">x</button>
            </li>
        </ul>
    </div>
</template>


<script>
export default {
    data() {
        return {
            newTodo: '',
            todos: []
        };
    },
    methods: {
        addTodo() {
            if (this.newTodo.trim() !== '') {
                this.todos.push({ text: this.newTodo, done: false });
                this.newTodo = '';
                this.saveTodos();
            }
        },
        removeTodo(index) {
            this.todos.splice(index, 1);
            this.saveTodos();
        },
        saveTodos() {
            localStorage.setItem('todos', JSON.stringify(this.todos));
        },
        loadTodos() {
            const savedTodos = localStorage.getItem('todos');
            if (savedTodos) {
            this.todos = JSON.parse(savedTodos);
            }
        }
    },
    mounted() {
        this.loadTodos();
    }
};
</script>


<style scoped>
    .todo-list {
        width: 300px;
        margin: 50px auto;
        text-align: center;
        background-color: #f9f9f9;
        border-radius: 10px;
        padding: 30px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    input[type="text"] {
        width: 100%;
        padding: 10px;
        margin-bottom: 20px;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1) inset;
    }
    li {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 10px;
        padding: 10px;
        border: 1px solid #ccc;
        border-radius: 4px;
        background-color: #fff;
        box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    }
    .done {
        text-decoration: line-through;
        color: #aaa;
    }
    button {
        background: none;
        border: none;
        color: red;
        cursor: pointer;
        font-size: 16px;
    }
    button:active {
        color: darkred;
}

</style>
