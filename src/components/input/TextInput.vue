<template>
    <input :id=id type="text" :value="modelValue" @change="updateValue" class="form-control">
</template>

<script setup>
    const { id, modelValue } = defineProps(['id', 'modelValue'])
    const emit = defineEmits()

    const updateValue = (event) => {
        emit('update:modelValue', event.target.value)
    }
</script>