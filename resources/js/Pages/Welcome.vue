<template>
    <!-- <Head title="Hoşgeldin •" /> -->
    <div
        class="relative sm:flex sm:justify-center sm:items-center min-h-screen bg-center bg-gray-50 bg-dots-darker selection:bg-gray-200 selection:text-gray-800"
    >
        <div v-if="canLogin" class="sm:fixed sm:top-0 sm:right-0 p-6 text-right">
            <Link
                v-if="$page.props.auth.user"
                :href="route('myFiles')"
                class="px-3 py-2 rounded-md bg-neutral-800 text-gray-100 font-semibold hover:text-gray-200 focus:outline focus:outline-2 focus:rounded-sm focus:outline-gray-400"
            >
                Panele Git
            </Link>
            <template v-else>
                <Link
                    :href="route('login')"
                    class="font-semibold text-gray-600 hover:text-gray-900 focus:outline focus:outline-2 focus:rounded-sm focus:outline-gray-400"
                >
                    Giriş Yap
                </Link>

                <Link
                    v-if="canRegister"
                    :href="route('register')"
                    class="ml-4 font-semibold text-gray-600 hover:text-gray-900 focus:outline focus:outline-2 focus:rounded-sm focus:outline-gray-400"
                >
                    Kayıt Ol
                </Link>
            </template>
        </div>

        <div class="max-w-7xl mx-auto p-6 lg:p-8">
            <div class="flex justify-center">
                <ApplicationLogo
                    class="sm:max-w-lg md:w-2/3 lg:w-1/3 fill-gray-700 hover:fill-black transition-all"
                />
            </div>

            <div class="mt-16">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 lg:gap-8">
                    <div class="scale-100 p-6 bg-white from-gray-700/50 via-transparent rounded-lg shadow-2xl shadow-gray-500/20 flex motion-safe:hover:scale-[1.01] transition-all duration-250 focus:outline focus:outline-2 focus:outline-gray-400">
                        <div>
                            <h2 class="mt-3 text-xl font-semibold text-gray-900">Sizin Kadar Hızlı</h2>

                            <p class="mt-4 text-gray-500 text-sm leading-relaxed">
                                simurg.space; barındırma alanı, kullanıcı sayısı, tek seferde yüklenen dosya boyutu ve sayısında herhangi bir sınırlama dayatmaz. Sunucunuzun karşıladığı ölçüde tüm bu değerleri özgürce belirleme hakkına sahipsiniz.
                            </p>
                        </div>
                    </div>

                    <div
                        class="scale-100 p-6 bg-white from-gray-700/50 via-transparent rounded-lg shadow-2xl shadow-gray-500/20 flex motion-safe:hover:scale-[1.01] transition-all duration-250 focus:outline focus:outline-2 focus:outline-gray-400"
                    >
                        <div>
                            <h2 class="mt-3 text-xl font-semibold text-gray-900">Hızlı ve Gelişmiş Altyapı Desteği</h2>

                            <p class="mt-4 text-gray-500 text-sm leading-relaxed">
                                simurg.space; Laravel, Vue.Js ve Inertia teknolojileri kullanılarak geliştirilmiş API tabanlı çalışan bir dosya barındırma ve paylaşım hizmetidir. Optimizasyon sonuçlarını <a href="#" class="hover:text-gray-700 underline">buradan</a> inceleyebilirsiniz.
                            </p>
                        </div>
                    </div>

                    <div
                        class="scale-100 p-6 bg-white from-gray-700/50 via-transparent rounded-lg shadow-2xl shadow-gray-500/20 flex motion-safe:hover:scale-[1.01] transition-all duration-250 focus:outline focus:outline-2 focus:outline-gray-400"
                    >
                        <div>
                            <h2 class="mt-3 text-xl font-semibold text-gray-900">Ekip Çalışmasına Uygun</h2>

                            <p class="mt-4 text-gray-500 text-sm leading-relaxed">
                                Dosya, klasör oluşturun veya yükleyin ve ekip arkadaşlarınızla paylaşın ve ortak çalışma alanları oluşturun.
                            </p>
                        </div>
                    </div>

                    <div
                        class="scale-100 p-6 bg-white from-gray-700/50 via-transparent rounded-lg shadow-2xl shadow-gray-500/20 flex motion-safe:hover:scale-[1.01] transition-all duration-250 focus:outline focus:outline-2 focus:outline-gray-400"
                    >
                        <div>
                            <h2 class="mt-3 text-xl font-semibold text-gray-900">Geliştirmeye Devam Ediyoruz</h2>

                            <p class="mt-4 text-gray-500 text-sm leading-relaxed">
                                Kendi takvimimize ve sizlerden aldığımız geri dönüşlere odaklanarak uygulamayı sürekli olarak geliştirmeye devam ediyoruz.!
                            </p>
                        </div>
                    </div>
                </div>
            </div>

            <div class="flex justify-center mt-16 px-6 sm:items-center sm:justify-between">
                <div class="text-center text-sm text-gray-500 sm:text-left">
                    <div class="flex items-center gap-4">
                        <a
                            href="https://simurg.de"
                            class="group inline-flex items-center hover:text-gray-700 focus:outline focus:outline-2 focus:rounded-sm focus:outline-gray-400"
                        >
                            <ApplicationLogo class="h-5 fill-gray-500 hover:fill-gray-700" />
                        </a>
                    </div>
                </div>

                <div class="ml-4 text-center text-sm text-gray-500 sm:text-right sm:ml-0">
                    simurg.space<sup>v{{ appVersion }}</sup>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import {Head, Link, usePage} from '@inertiajs/vue3';
import ApplicationLogo from "@/Components/ApplicationLogo.vue";
import {onMounted} from "vue";

defineProps({
    canLogin: {
        type: Boolean
    },
    canRegister: {
        type: Boolean
    },
    appVersion: {
        type: String,
        required: true
    }
})

onMounted(() => {
    const page = usePage()
    if (page.props.isAuthenticated) {
        Inertia.location('myFiles')
    }
})
</script>

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
