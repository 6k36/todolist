<script setup lang="ts">
import { ref } from 'vue';

// 待办事项列表（响应式数据）
const todoList = ref<string[]>([]);
// 新增待办的输入内容
const newTodo = ref('');

// 添加待办事项
const addTodo = () => {
  if (newTodo.value.trim() === '') return;
  todoList.value.push(newTodo.value);
  newTodo.value = ''; // 清空输入框
};

// 删除待办事项
const deleteTodo = (index: number) => {
  todoList.value.splice(index, 1);
};

// 清空所有待办事项
const clearAll = () => {
  todoList.value = [];
};
</script>

<template>
  <div class="todo-container">
    <h1>本周待办事项</h1>
    <ul class="todo-list" v-if="todoList.length > 0">
      <li v-for="(todo, index) in todoList" :key="index">
        {{ todo }}
        <button class="delete-btn" @click="deleteTodo(index)">删除</button>
      </li>
    </ul>
    <div class="input-area" v-else>
      暂无待办事项，快添加一个吧~
    </div>
    <div class="input-area">
      <input 
        type="text" 
        v-model="newTodo" 
        placeholder="请输入待办事项..." 
        @keypress.enter="addTodo"
      >
      <button @click="addTodo">添加</button>
    </div>
    <button class="clear-btn" @click="clearAll" v-if="todoList.length > 0">清空所有</button>
  </div>
</template>

<style scoped>
.todo-container {
  width: 400px;
  margin: 50px auto;
  padding: 20px;
  background: #f5f5f5;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin-bottom: 20px;
}

.todo-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background: #fff;
  border-radius: 4px;
  margin-bottom: 10px;
}

.delete-btn {
  background: #dc3545;
  color: #fff;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}

.input-area {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 10px;
  border: 2px solid #007bff;
  border-radius: 4px;
  outline: none;
}

button {
  padding: 10px 20px;
  cursor: pointer;
  border: none;
  border-radius: 4px;
}

button:not(.delete-btn) {
  background: #007bff;
  color: #fff;
}

.clear-btn {
  display: block;
  width: 100%;
  background: #6c757d;
  color: #fff;
}
</style>
