<script setup>
import { Icon } from "@iconify/vue";
defineProps({
    todoItem: {
        type: Object,
        required: true
    },
    index:{
        type: Number,
        required: true
    }
});

defineEmits([
    'toggle-complete',
    'toggle-editing',
    'toggle-save',
    'toggle-delete'
])
</script>
<template>
    <li class="list-group-item">
        <div class="input-group mb-3">
            <div class="input-group-prepend">
                <span class="input-group-text">
                    <input type="checkbox" :id="'check-'+todoItem.id" :checked="todoItem.isCompleted" @input="$emit('toggle-complete', index)">
                </span>
            </div>
            <input v-if="todoItem.isEditing" type="text" class="form-control" :value="todoItem.todo" @input="$emit('toggle-save', index, $event.target.value)"/>
            <span v-else class="form-control" :class="{'todo-completed': todoItem.isCompleted}">{{ todoItem.todo }}</span>
            <div class="input-group-append">
                <span class="input-group-text">
                    <Icon v-if="todoItem.isEditing" icon="ph:check-circle" class="icon check-icon" color="41b080" width="22"  @click="$emit('toggle-editing', index)"/>
                    <Icon v-else icon="ph:pencil-fill" class="icon edit-icon" color="41b080" width="22" @click="$emit('toggle-editing', index)"/>
                    <Icon icon="ph:trash" class="icon trash-icon" color="f95e5e" width="22" @click="$emit('toggle-delete', todoItem.id)"/>
                </span>
            </div>
        </div>
    </li>
</template>
<style scoped>
.todo-completed{
    text-decoration: line-through;
}
</style>