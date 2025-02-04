<script setup>
const model = defineModel()

</script>
<template>
    <button class="px-4 py-2 text-sm font-medium text-white bg-black border disabled:text-gray-600">
        <slot></slot>
    </button>
</template>