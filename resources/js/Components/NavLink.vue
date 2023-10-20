<script setup>
import { computed } from 'vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({
    href: {
        type: String,
        required: true,
    },
    active: {
        type: Boolean,
    },
});

const classes = computed(() =>
    props.active
        ? 'flex items-center justify-center px-5 py-2 rounded-lg border-indigo-400 dark:border-gray-600 text-sm font-medium leading-5 text-indigo-700 dark:text-indigo-900 bg-indigo-100 dark:bg-neutral-700 dark:text-gray-200 focus:outline-none focus:border-indigo-700 transition duration-150 ease-in-out'
        : 'flex items-center justify-center px-5 py-2 rounded-lg border-transparent text-sm font-medium leading-5 text-gray-700 dark:text-gray-400 hover:text-gray-700 hover:border-gray-300 focus:outline-none focus:text-gray-700 focus:border-gray-300 transition duration-150 ease-in-out'
);
</script>

<template>
    <Link :href="href" :class="classes">
        <slot />
    </Link>
</template>
