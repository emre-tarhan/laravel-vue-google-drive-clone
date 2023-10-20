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
        ? 'block w-full pl-3 pr-4 py-2 text-left text-sm font-medium text-blue-400 bg-indigo-50 dark:bg-indigo-900 dark:text-indigo-200 focus:outline-none focus:text-indigo-800 focus:bg-indigo-100 dark:focus:bg-indigo-800 dark:focus:text-indigo-200 rounded-md mb-1 focus:border-indigo-700 transition duration-150 ease-in-out'
        : 'block w-full pl-3 pr-4 py-2 text-left text-sm font-medium text-gray-800 dark:text-gray-300 hover:text-gray-800 dark:hover:text-gray-300 rounded-md hover:bg-gray-50 dark:hover:bg-neutral-800 hover:border-gray-300 focus:outline-none focus:text-gray-800 dark:focus:bg-neutral-900 dark:focus:text-neutral-300 focus:bg-gray-50 dark:focus focus:border-gray-300 transition duration-150 ease-in-out'
);
</script>

<template>
    <Link :href="href" :class="classes">
        <slot />
    </Link>
</template>
