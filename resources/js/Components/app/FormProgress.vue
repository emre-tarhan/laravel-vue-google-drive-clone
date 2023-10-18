<template>
    <div v-if="form.progress" class="absolute border-gray-600 border right-8 bottom-4 bg-white shadow-lg rounded-md flex flex-col w-[240px] p-2">
        <div class="text-xs mb-2">{{ form.files.length }} adet dosya yükleniyor..</div>
        <div class="h-2 bg-gray-100 rounded">
            <div class="h-full bg-blue-600 rounded transition-all" :style="{width: form.progress.percentage+'%'}"></div>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    form: Object
})
</script>


<style scoped>

</style>
