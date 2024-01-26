<script setup>
import { reactive, /*ref,*/ defineEmits } from 'vue';
import ButtonComponent from '@/components/ButtonComponent.vue';
//const todo = ref("testing"); // for premitive you may use ref("value") for object use reactive({})
// console.log(todo.value); // if you want to access outside the template
const todoCreateComponentState = reactive({
    todo: "",
    invalid: false,
    error: null,
});
console.log(todoCreateComponentState.todo);


const emits = defineEmits(['create-todo-event']);
const createTodo = () => {
    todoCreateComponentState.invalid = false;
    if(todoCreateComponentState.todo.trim() != ""){
        emits("create-todo-event", todoCreateComponentState.todo);
        todoCreateComponentState.todo = "";
        return;
    }

    todoCreateComponentState.error = "Todo can not be blank";
    todoCreateComponentState.invalid = true;
}

</script>
<template>
    <div class="input-group mb-3">
        <!--<input type="text" class="form-control" v-model="todo">-->
        <input type="text" class="form-control" v-on:keyup.enter="createTodo()" v-model="todoCreateComponentState.todo" :class="{'border border-danger': todoCreateComponentState.invalid}">
        <div class="input-group-append">
            <ButtonComponent v-on:click="createTodo()">Create Todo</ButtonComponent>
        </div>
    </div>
    <div class="alert alert-danger" v-if="todoCreateComponentState.invalid">{{ todoCreateComponentState.error}}</div>

    <div style="display: none;">{{ todoCreateComponentState.todo }}</div>
</template>
<style scoped></style>