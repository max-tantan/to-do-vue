<script setup>
import { ref, computed } from 'vue';

const todos = ref([]);
const newTodo = ref('');
const filter = ref('all');

const addTodo = () => {

//mengecek apakah input kosong atau tidak
if(newTodo.value.trim() === '') {
    alert('todo tidak boleh kosong');
    return;
}

//menambahkan todo baru ke dalam list
const todoItem = {
    id: Date.now(),
    text: newTodo.value,
    completed: false
}

//push todo baru ke dalam array todos
todos.value.push(todoItem);
newTodo.value = '';
}

const filteredTodos = computed(() => {
    return todos.value
})

//delete todo
const deleteTodo = (id) => {
    todos.value = todos.value.filter(t => t.id !== id);
}

//total todo dan status
const totalTodos = computed(() => 
todos.value.length
);

const completedTodos =computed(() => 
todos.value.filter(t => t.completed).length
);

const activeTodos = computed(() =>
totalTodos.value - completedTodos.value
);

</script>
<template>
<h1>Todo</h1>

<div class="todo-input">
    <input 
    type="text" 
    v-model="newTodo" 
    placeholder="Add a new todo..." 
    @keyup.enter="addTodo"
    />
    <button @click="addTodo">Add Todo</button>
</div>

<div class="todo-stats">
    <div class="stats">
        <strong>Total: {{ totalTodos }}</strong>
    </div>
    <div class="stats">
        <strong>Completed: {{ completedTodos }}</strong>
    </div>
    <div class="stats">
        <strong>Active: {{ activeTodos }}</strong>
    </div>
</div>
<div class="to-do-list">
    <ul>
        <li v-for="todo in filteredTodos" :key="todo.id">
            <input type="checkbox" v-model="todo.completed" />
            <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
            <button @click="deleteTodo(todo.id)">Hapus</button>
        </li>
    </ul>
</div>


</template>

<style scoped>
.completed {
    text-decoration: line-through;
    color: gray;
}
</style>