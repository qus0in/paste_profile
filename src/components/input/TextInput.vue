<template>
    <input :id=id type="text" :value="modelValue" @change="updateValue" class="form-control" :placeholder=placeholder>
</template>

<script setup>
    const { id, modelValue, placeholder } = defineProps(['id', 'modelValue', 'placeholder'])
    const emit = defineEmits()

    const updateValue = (event) => {
        emit('update:modelValue', event.target.value)
    }
</script>