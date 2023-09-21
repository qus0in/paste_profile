<template>
    <select :id=componentId :value="modelValue" @change="updateValue" class="form-control">
        <option v-for="item in items" :key="item" :value="item">{{ item }}</option>
    </select>
</template>

<script setup>
    const {
        modelValue, componentId, items
    } = defineProps(['id', 'modelValue', 'items'])
    const emit = defineEmits()
    const updateValue = (event) => {
        emit('update:modelValue', event.target.value)
    }
</script>