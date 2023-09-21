<template>
    <MdEditor
      class="md-editor"
      language="en-US"
      previewTheme="github"
      codeThem="github"
      noUploadImg=true
      v-model="modelValue"
    />
</template>

<script setup>
    import { MdEditor } from 'md-editor-v3';
    import 'md-editor-v3/lib/style.css';
    import { ref } from 'vue'

    const props = defineProps(['modelValue'])
    const modelValue = ref(props.modelValue)
    
</script>

<style>
    .md-editor {
        height: 300px;
    }
</style>