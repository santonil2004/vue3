<script setup>
import TodoCreateComponent from '@/components/TodoCreateComponent.vue';
import TodoItemComponent from '@/components/TodoItemComponent.vue';
import { Icon } from '@iconify/vue';
import { uid } from 'uid';
import { ref } from 'vue';
const todoList = ref([]);

const createTodoListner = (todo) => {
    console.log(">>" + todo);
    todoList.value.push({
        id: uid(),
        todo: todo,
        isCompleted: null,
        isEditing: null
    })
}

const toggleCompleteListner = (index) => {
    console.log(index)
}

</script>
<template>
    <h1>Create todo</h1>
    <div class="col">
        <div class="col-6">
            <TodoCreateComponent @create-todo-event="createTodoListner" />
            <hr />
            <ul class="list-group" v-if="todoList.length">
                <TodoItemComponent v-for="(todoItem, index) in todoList" v-bind:key="todoItem.id" :todoItem="todoItem" :index="index" @toggle-complete="toggleCompleteListner"/>
            </ul>

            <div v-else class="alert alert-info">
                <Icon icon="noto-v1:sad-but-relieved-face" />
                <span class="pl-1">You have no todo's to complete! Add one!</span>
            </div>
        </div>
        <div class="col-6"></div>
    </div>
</template>
<style scoped></style>