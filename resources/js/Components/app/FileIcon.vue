<template>
    <span class="w-6 h-6 inline-flex items-center justify-center mr-2">
        <FolderIcon class="max-w-full text-gray-800 dark:text-gray-300" v-if="file.is_folder" />
        <template v-else>
            <img class="max-w-full" v-if="isAudio(file)" :src="`/images/icons/mp3.png`">
            <img class="max-w-full" v-else-if="isImage(file)" :src="`/images/icons/image.png`">
            <img class="max-w-full" v-else-if="isPDF(file)" :src="`/images/icons/pdf.png`">
            <img class="max-w-full" v-else-if="isText(file)" :src="`/images/icons/txt.png`">
            <img class="max-w-full" v-else-if="isVideo(file)" :src="`/images/icons/video.png`">
            <img class="max-w-full" v-else-if="isZip(file)" :src="`/images/icons/zip.png`">
            <img class="max-w-full" v-else="isWord(file)" :src="`/images/icons/txt.png`">
        </template>
    </span>
</template>

<script setup>
    import {FolderIcon} from "@heroicons/vue/20/solid/index.js";
    import {isAudio, isImage, isPDF, isText, isVideo, isWord, isZip} from "@/Helper/file-helper.js";

    const {file} = defineProps({
        file: Object
    })
</script>

<style scoped>

</style>
