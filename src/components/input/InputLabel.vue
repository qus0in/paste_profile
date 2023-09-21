<template>
    <label :for=_for class="input-group-text">{{ label }}</label>
</template>

<script setup>
    const props = defineProps(['for', 'label'])
    const _for = props.for + '-' + props.label
    const label = props.label
</script>

<style scoped>
label {
  width: 100px;
}
</style>