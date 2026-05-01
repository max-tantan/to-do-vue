<script setup>
const addTodo = ref('');

if(newTodo.value.trim() === '') {
    alert('todo tidak boleh kosong');
    return;
}
</script>
<template>
<h1>Website To-Do-List</h1>
<div class="todo-input">
    <input type="text" v-model="addTodo" placeholder="Add a new todo..." @keyup.enter="addTodo"
    />
    <button @click="addTodo">Add Todo</button>
</div>
</template>