<template>
    <button
        @click="onClick"
        class="inline-flex items-center px-4 py-2 text-sm font-medium text-gray-900 bg-white border border-gray-200 dark:text-gray-300 dark:bg-neutral-800 dark:border-neutral-800 dark:hover:bg-neutral-950 dark:hover:text-gray-300 transition-all rounded-md ml-1 hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4 mr-2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M9 9l6-6m0 0l6 6m-6-6v12a6 6 0 01-12 0v-3" />
        </svg>
        Geri Al
    </button>
    <ConfirmationDialog
        :show="showConfirmationDialog"
        message="Seçili dosyalar geri alınacak, emin misin?"
        @cancel="onCancel"
        @confirm="onConfirm"
    />
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

    const showConfirmationDialog = ref(false)

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

    const emit = defineEmits(['restore'])

    function onClick ()
    {
        if (!props.allSelected && !props.selectedIds.length) {
            showErrorDialog('Bu işlem için minimum bir adet öğe seçmelisin 😃')
            return

        }
        showConfirmationDialog.value = true
    }

    function onCancel ()
    {
        showConfirmationDialog.value = false
    }

    function onConfirm ()
    {
        if (props.allSelected) {
            form.all = true
        } else {
            form.ids = props.selectedIds
        }

        form.post(route('file.restore'), {
            onSuccess: () => {
                showConfirmationDialog.value = false
                emit('restore')
                if (props.allSelected) {
                    showSuccessNotification('Bu klasördeki tüm dosyaları kurtardın')
                } else {
                    showSuccessNotification(`${props.selectedIds.length} adet dosya kurtarıldı`)
                }
            }
        })
    }

</script>

<style scoped>

</style>
