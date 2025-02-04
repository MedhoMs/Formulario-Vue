<script setup>


defineProps ({
    options: {
        type:Array,
        required: true
    }
    
    
})

</script>
<template>
    <datalist class="bg-white/30 backdrop-blur-lg rounded-lg p-1">
        <option v-for="option in options" :value="option.value" :key="option.value" class="text-black"></option>
    </datalist>
</template>