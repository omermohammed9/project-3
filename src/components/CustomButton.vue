<script setup>
defineProps({
    label : {
        type: String,
        required: true,
        default: "Click Me",
        validator(value){
            return value.length > 3;
        }
    }
});

</script>

<template>
  <button class="rounded bg-indigo-300 px-3 py-2 font-bold text-white hover:bg-indigo-800 transition-all">
      {{label}}
      
      </button>
</template>


<!-- 
<style scoped>

</style> -->