<script setup>
import DangerButton from '@/Components/DangerButton.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import Modal from '@/Components/Modal.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { useForm } from '@inertiajs/vue3';
import { nextTick, ref } from 'vue';

const confirmingUserDeletion = ref(false);
const passwordInput = ref(null);

const form = useForm({
    password: '',
});

const confirmUserDeletion = () => {
    confirmingUserDeletion.value = true;

    nextTick(() => passwordInput.value.focus());
};

const deleteUser = () => {
    form.delete(route('profile.destroy'), {
        preserveScroll: true,
        onSuccess: () => closeModal(),
        onError: () => passwordInput.value.focus(),
        onFinish: () => form.reset(),
    });
};

const closeModal = () => {
    confirmingUserDeletion.value = false;

    form.reset();
};
</script>

<template>
    <section class="space-y-6">
        <header>
            <h2 class="text-lg font-medium text-gray-900 dark:text-neutral-300">Hesabını Sil</h2>

            <p class="mt-1 text-sm text-gray-600 dark:text-neutral-400">
                Hesabınız silindiğinde, tüm kaynaklar ve veriler kalıcı olarak silinecektir. Hesabınızı silmeden önce saklamak istediğiniz herhangi bir veriyi veya bilgiyi indirmenizi öneririz.
            </p>
        </header>

        <DangerButton @click="confirmUserDeletion">HESABINIZI KALICI OLARAK SİLİN</DangerButton>

        <Modal :show="confirmingUserDeletion" @close="closeModal">
            <div class="p-6">
                <h2 class="text-lg font-medium text-gray-900 dark:text-neutral-300">
                    Hesabını silmek istediğine emin misin?
                </h2>

                <p class="mt-1 text-sm text-gray-600 dark:text-neutral-400">
                    Hesabınız bir kez silindiğinde, tüm kaynaklar ve verileri kalıcı olarak silinecektir. Hesabınızı kalıcı olarak silmek istediğinizi onaylamak için lütfen şifrenizi girin.
                </p>

                <div class="mt-6">
                    <InputLabel for="password" value="Mevcut Şifre" class="sr-only" />

                    <TextInput
                        id="password"
                        ref="passwordInput"
                        v-model="form.password"
                        type="password"
                        class="mt-1 block w-3/4"
                        placeholder="Mevcut şifreniz"
                        @keyup.enter="deleteUser"
                    />

                    <InputError :message="form.errors.password" class="mt-2" />
                </div>

                <div class="mt-6 flex justify-end">
                    <SecondaryButton @click="closeModal"> VAZGEÇ </SecondaryButton>

                    <DangerButton
                        class="ml-3"
                        :class="{ 'opacity-25': form.processing }"
                        :disabled="form.processing"
                        @click="deleteUser"
                    >
                        HESABIMI SİL
                    </DangerButton>
                </div>
            </div>
        </Modal>
    </section>
</template>
