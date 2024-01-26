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
    'toggle-complete'
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
            <input v-if="todoItem.isEditing" type="text" class="form-control" :value="todoItem.todo" />
            <span v-else class="form-control">{{ todoItem.todo }}</span>
            <div class="input-group-append">
                <span class="input-group-text">
                    <Icon v-if="todoItem.isEditing" icon="ph:check-circle" class="icon check-icon" color="41b080" width="22" />
                    <Icon v-else icon="ph:pencil-fill" class="icon edit-icon" color="41b080" width="22" />
                    <Icon icon="ph:trash" class="icon trash-icon" color="f95e5e" width="22" />
                </span>
            </div>
        </div>
    </li>
</template>
<style scoped></style>