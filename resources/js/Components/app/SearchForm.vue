<template>
    <form class="w-[600px] h-[80px] flex items-center">
        <TextInput
            type="text"
            class="block w-full mr-2"
            :class="{'bg-neutral-900 border-neutral-950' : darkMode}"
            v-model="form.search"
            autocomplete
            placeholder="Dosya adı veya klasör arayın.."
        />
    </form>
</template>

<script setup>
    import TextInput from "@/Components/TextInput.vue";
    import {useForm} from "@inertiajs/vue3";
    import {onMounted, ref} from "vue";
    import {DISPLAY_MODE, emitter} from "@/event-bus.js";

    const darkMode = ref(localStorage.getItem('darkMode') === 'true');

    const form = useForm({
        search: ''
    })

    onMounted(() => {
        emitter.on(DISPLAY_MODE, (newDarkMode) => {
            darkMode.value = newDarkMode
        })
    })
</script>

<style scoped>

</style>
