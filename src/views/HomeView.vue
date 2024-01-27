<script setup>
import TodoCreateComponent from '@/components/TodoCreateComponent.vue';
import TodoItemComponent from '@/components/TodoItemComponent.vue';
import { Icon } from '@iconify/vue';
import { uid } from 'uid';
import { ref, watch, computed } from 'vue';
const todoList = ref([]);

const saveInLocalStorage = () => {
    localStorage.setItem("todoList", JSON.stringify(todoList.value));
}

const fetchFromLocalStorage = () => {
    const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
    if (savedTodoList) {
        todoList.value = savedTodoList;
    }
};

fetchFromLocalStorage();

watch(todoList, () => {
    saveInLocalStorage();
}, {
    deep: true
})

const todosCompleted = computed(() => {
    return todoList.value.every((todo) => todo.isCompleted);
});

const onCreateTodo = (todo) => {
    console.log(">>" + todo);
    todoList.value.push({
        id: uid(),
        todo: todo,
        isCompleted: null,
        isEditing: null
    })
}

const onToggleComplete = (index) => {
    todoList.value[index].isCompleted = !todoList.value[index].isCompleted;
}

const onToggleEditing = (index) => {
    todoList.value[index].isEditing = !todoList.value[index].isEditing;
}

const onToggleSave = (index, updatedTodo) => {
    todoList.value[index].todo = updatedTodo;
}

const onToggleDelete = (todoId) => {
    todoList.value = todoList.value.filter((todo) => {
        return todo.id != todoId
    })
}

</script>
<template>
    <h1>Create todo</h1>
    <div class="col">
        <div class="col-6">
            <TodoCreateComponent @create-todo-event="onCreateTodo" />
            <hr />
            <div v-if="todosCompleted && todoList.length > 0" class="alert alert-success mt-1 md-1">
                <Icon icon="noto-v1:party-popper" />
                <span class="pl-1">You have completed all your todos!</span>
            </div>
            <ul class="list-group" v-if="todoList.length">
                <TodoItemComponent v-for="(todoItem, index) in todoList" v-bind:key="todoItem.id" :todoItem="todoItem"
                    :index="index" @toggle-complete="onToggleComplete" @toggle-editing="onToggleEditing"
                    @toggle-save="onToggleSave" @toggle-delete="onToggleDelete" />
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