<script setup lang="ts">
    const props = defineProps(['selectedName']);
    const emit = defineEmits(['remove']);

    const removeName = (name: string) => {
        emit('remove', name);
    };

</script>
<template>
    <div class="bg-white p-4 rounded shadow-md" v-for="name in selectedName" :key="name">
        <span class="text-lg font-semibold mb-4 text-center block">{{name}}</span>
        <button @click="removeName(name)" class="text-red-500">X</button>
    </div>
</template>