<template>
    <nav class="min-w-[200px]">
            <Link :href="route('myFiles')" class="h-[80px] px-3 flex items-center gap-3">
                <ApplicationLogo
                    class="block w-5 w-auto fill-gray-900 dark:fill-gray-200 text-gray-800"
                />
            </Link>
        <div class="px-3">
            <CreateNewDropdown />

            <div class="py-3">
                <NavLink :href="route('myFiles')" :active="$page.url === '/my-files'">Dosyalarım</NavLink>
                <NavLink href="/">Paylaşılanlar</NavLink>
                <NavLink href="/">Gönderilenler</NavLink>
                <NavLink href="/">Çöp Kutusu</NavLink>
            </div>
        </div>
    </nav>
</template>

<script setup>
    import {Link} from "@inertiajs/vue3";
    import ApplicationLogo from "@/Components/ApplicationLogo.vue";
    import CreateNewDropdown from "@/Components/app/CreateNewDropdown.vue";
    import NavLink from "@/Components/NavLink.vue";
</script>

<style scoped>

</style>
