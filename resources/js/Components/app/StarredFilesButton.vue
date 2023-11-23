<template>
    <button
        @click="onClick"
        class="inline-flex items-center px-4 py-2 text-sm font-medium text-gray-900 bg-white border border-gray-200 dark:text-neutral-300 dark:bg-neutral-800 dark:border-neutral-800 dark:hover:bg-neutral-950 dark:hover:text-gray-300 transition-all rounded-md ml-1 hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4 mr-2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M11.48 3.499a.562.562 0 011.04 0l2.125 5.111a.563.563 0 00.475.345l5.518.442c.499.04.701.663.321.988l-4.204 3.602a.563.563 0 00-.182.557l1.285 5.385a.562.562 0 01-.84.61l-4.725-2.885a.563.563 0 00-.586 0L6.982 20.54a.562.562 0 01-.84-.61l1.285-5.386a.562.562 0 00-.182-.557l-4.204-3.602a.563.563 0 01.321-.988l5.518-.442a.563.563 0 00.475-.345L11.48 3.5z" />
        </svg>
        Favoriye Ekle
    </button>
    <span class="absolute bottom-5 right-7 text-sm bg-white border shadow-lg py-2 px-4 rounded-lg" v-if="selectedIds.length > 0">{{selectedIds.length}} öğe seçildi</span>
</template>

<script setup>

    import ConfirmationDialog from "@/Components/ConfirmationDialog.vue";
    import {ref} from "vue";
    import {useForm, usePage} from "@inertiajs/vue3";
    import {showErrorDialog, showSuccessNotification} from "@/event-bus.js";

    const page = usePage()
    const form = useForm({
        all: null,
        ids: [],
        parent_id: null
    })

    const props = defineProps({
        allSelected: {
            type: Boolean,
            required: false,
            default: false
        },
        selectedIds: {
            type: Array,
            required: false
        }
    })

    function onClick () {
        if (!props.allSelected && !props.selectedIds.length) {
            showErrorDialog('Bu işlem için minimum bir adet öğe seçmelisin 😃')
            return
        }

        form.parent_id = page.props.folder.id
        if (props.allSelected) {
            form.all = true
        } else {
            form.ids = props.selectedIds
        }

        form.post(route('file.star'), {
            onSuccess: () => {
                form.ids = [];
                showSuccessNotification('Seçili dosyaları favoriledin!')
            }
        })
    }

</script>

<style scoped>

</style>
