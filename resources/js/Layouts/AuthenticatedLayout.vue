<template>
    <div
        :class="{'h-screen': page.url !== '/profile'}"
        class="bg-gray-50 dark:bg-neutral-900 bg-dots-darker dark:bg-dots-lighter flex w-full gap-4"
    >
        <Navigation
            class="bg-white dark:bg-neutral-950 ring-1 ring-inset ring-white dark:ring-black rounded-md ml-2 my-2"/>

        <main
            @drop.prevent="handleDrop"
            @dragover.prevent="onDragOver"
            @dragleave.prevent="onDragLeave"
            class="flex flex-col flex-1 pr-4 overflow-hidden"
            :class="dragOver ? 'dropzone' : ''"
        >
            <template v-if="dragOver" class="text-gray-600 text-center py-6 text-md">
                Dosyaları yüklemek için buraya bırakın
            </template>
            <template v-else>
                <div class="flex items-center justify-between w-full bg-white rounded-md my-2 px-6 ring-1 ring-inset ring-white dark:ring-black dark:bg-neutral-950">
                    <SearchForm/>
                    <UserSettingsDropdown/>
                </div>
                <div class="flex flex-1 flex-col overflow-hidden bg-white rounded-md p-6 mb-2 ring-1 ring-inset ring-white dark:ring-black dark:bg-neutral-950">
                    <slot/>
                </div>
            </template>
        </main>
    </div>
    <ErrorDialog/>
    <FormProgress :form="fileUploadForm"/>
</template>

<script setup>
import Navigation from "@/Components/app/Navigation.vue";
import SearchForm from "@/Components/app/SearchForm.vue";
import UserSettingsDropdown from "@/Components/app/UserSettingsDropdown.vue";
import {onMounted, ref} from "vue";
import {emitter, FILE_UPLOAD_STARTED, showErrorDialog} from "@/event-bus.js";
import {useForm, usePage} from "@inertiajs/vue3";
import FormProgress from "@/Components/app/FormProgress.vue";
import ErrorDialog from "@/Components/ErrorDialog.vue";

const page = usePage();

const fileUploadForm = useForm({
    files: [],
    relative_paths: [],
    parent_id: null
})

const dragOver = ref(false)

function onDragOver() {
    dragOver.value = true
}

function onDragLeave() {
    dragOver.value = false
}

function handleDrop(ev) {
    dragOver.value = false
    const files = ev.dataTransfer.files
    console.log(files)
    if (!files.length) {
        return
    }

    uploadFiles(files)
}

function uploadFiles(files) {
    fileUploadForm.parent_id = page.props.folder.id
    fileUploadForm.files = files
    fileUploadForm.relative_paths = [...files].map(f => f.webkitRelativePath)

    fileUploadForm.post(route('file.store'), {
        preserveScroll: true,
        onSuccess: () => {

        },
        onError: errors => {
            let message = '';

            if (Object.keys(errors).length > 0) {
                message = errors[Object.keys(errors)[0]]
            } else {
                message = 'Dosya yüklenirken bir hata oldu 😓 lütfen tekrar deneyin.'
            }
            showErrorDialog(message)
        },
        onFinish: () => {
            fileUploadForm.clearErrors()
            fileUploadForm.reset()
        }
    })
}

onMounted(() => {
    emitter.on(FILE_UPLOAD_STARTED, uploadFiles)
})
</script>

<style scoped>
.dropzone {
    width: 80%;
    height: 70%;
    margin-top: 5vh;
    border-radius: 1.5rem;
    color: #8D8D8D;
    border: 2px dashed #808080FF;
    display: flex;
    align-items: center;
    justify-content: center;
    flex: none;
}
</style>
<style>
    .bg-dots-darker {
        background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(0,0,0,0.07)'/%3E%3C/svg%3E");
    }
    @media (prefers-color-scheme: dark) {
        .dark\:bg-dots-lighter {
            background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(255,255,255,0.07)'/%3E%3C/svg%3E");
        }
    }
</style>
