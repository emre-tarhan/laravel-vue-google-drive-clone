<template>
    <Menu as="div" class="relative block text-left">
        <MenuButton
            class="flex w-full justify-center gap-x-1.5 rounded-lg bg-white dark:bg-gray-800 dark:text-gray-300 px-3 py-2 text-sm font-semibold text-gray-900 shadow-md ring-1 ring-inset ring-gray-300 dark:ring-gray-800 dark:shadow-black transition-all duration-500 hover:bg-gray-50 dark:hover:bg-gray-900"
        >
            Yeni Oluştur

        </MenuButton>

        <transition
            enter-active-class="transition duration-100 ease-out"
            enter-from-class="transform scale-95 opacity-0"
            enter-to-class="transform scale-100 opacity-100"
            leave-active-class="transition duration-75 ease-in"
            leave-from-class="transform scale-100 opacity-100"
            leave-to-class="transform scale-95 opacity-0"
        >
            <MenuItems
                class="absolute right-0 mt-2 w-full origin-top-right divide-y divide-gray-100 dark:divide-neutral-800 rounded-md bg-white dark:bg-neutral-900 shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
            >
                <div class="px-1 py-1">
                    <MenuItem v-slot="{ active }">
                        <a href="#" @click.prevent="showCreateFolderModal"
                           class="text-gray-700 dark:text-neutral-400 block px-4 py-2 text-sm">
                            Klasör Oluştur
                        </a>
                    </MenuItem>
                </div>
                <div class="px-1 py-1">
                    <FileUploadMenuItem />
                    <FolderUploadMenuItem />
                </div>
            </MenuItems>
        </transition>
    </Menu>
    <CreateFolderModal v-model="createFolderModal" />
</template>

<script setup>
    import {Menu, MenuButton, MenuItem, MenuItems} from "@headlessui/vue";
    import CreateFolderModal from "@/Components/app/CreateFolderModal.vue";
    import {ref} from "vue";
    import FileUploadMenuItem from "@/Components/app/FileUploadMenuItem.vue";
    import FolderUploadMenuItem from "@/Components/app/FolderUploadMenuItem.vue";

    const createFolderModal = ref(false)
    function showCreateFolderModal()
    {
        createFolderModal.value = true
    }
</script>

<style scoped>

</style>
