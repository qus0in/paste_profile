<template>
    <div class="card p-4 my-2">
      <p class="display-6">
        {{ title }}
      </p>
      <div class="container py-2">
        <slot></slot>
        </div>
        </div>
</template>

<script setup>
    const props = defineProps(['title'])
    const title = props.title
</script>