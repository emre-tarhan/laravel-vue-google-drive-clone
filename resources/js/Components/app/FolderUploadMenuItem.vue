<template>
    <MenuItem v-slot="{ active }">
        <a class="text-gray-700 dark:text-neutral-400 block px-4 py-2 text-sm relative">
            Klasör Yükle
            <input
                @change="onChange"
                type="file"
                multiple
                class="absolute left-0 top-0 bottom-0 right-0 cursor-pointer opacity-0"
                directory webkitdirectory
            >
        </a>
    </MenuItem>
</template>

<script setup>
    import {MenuItem} from "@headlessui/vue";
    import {emitter, FILE_UPLOAD_STARTED} from "@/event-bus.js";

    function onChange (ev)
    {
        emitter.emit(FILE_UPLOAD_STARTED, ev.target.files)
    }
</script>

<style scoped>

</style>
