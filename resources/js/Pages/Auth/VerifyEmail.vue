<script setup>
import { computed } from 'vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const props = defineProps({
    status: {
        type: String,
    },
});

const form = useForm({});

const submit = () => {
    form.post(route('verification.send'));
};

const verificationLinkSent = computed(() => props.status === 'verification-link-sent');
</script>

<template>
    <GuestLayout>
        <Head title="E-Posta Doğrulama •" />

        <div class="mb-4 text-sm text-gray-600">
            Kaydolduğunuz için teşekkürler! Başlamadan önce, bağlantıya tıklayarak e-posta adresinizi doğrulayabilir misiniz?
            size e-posta gönderdik mi? E-postayı almadıysanız, size memnuniyetle bir tane daha göndeririz.
        </div>

        <div class="mb-4 font-medium text-sm text-green-600" v-if="verificationLinkSent">
            Kayıt sırasında verdiğiniz e-posta adresine yeni bir doğrulama bağlantısı gönderilmiştir.
        </div>

        <form @submit.prevent="submit">
            <div class="mt-4 flex items-center justify-between">
                <PrimaryButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Doğrulama E-postasını Yeniden Gönder
                </PrimaryButton>

                <Link
                    :href="route('logout')"
                    method="post"
                    as="button"
                    class="underline text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                    >Çıkış Yap</Link
                >
            </div>
        </form>
    </GuestLayout>
</template>
