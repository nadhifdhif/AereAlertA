<script setup>
import { reactive, ref } from 'vue';
import { Head, Link, router } from '@inertiajs/vue3';
import AppLogo from '@/Components/AppLogo.vue';
import Icon from '@/Components/Icon.vue';

const form = reactive({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
});

const showPassword = ref(false);
const showPasswordConfirmation = ref(false);
const processing = ref(false);

function submit() {
    processing.value = true;
    router.visit('/dashboard');
}
</script>

<template>
    <Head title="Create account" />

    <div class="flex min-h-screen items-center justify-center bg-gradient-to-b from-sky-50 via-slate-50 to-white px-4 py-12">
        <div class="w-full max-w-md rounded-2xl border border-slate-200 bg-white p-8 shadow-sm">
            <div class="flex flex-col items-center text-center">
                <AppLogo variant="dark" size="lg" />
                <p class="mt-2 text-xs uppercase tracking-wider text-slate-400">Air Quality &amp; Environmental Monitoring</p>
            </div>

            <div class="my-6 flex items-center gap-3">
                <span class="h-px flex-1 bg-slate-200" />
                <span class="text-xs italic text-slate-400">Create your account</span>
                <span class="h-px flex-1 bg-slate-200" />
            </div>

            <form class="space-y-5" @submit.prevent="submit">
                <div>
                    <label for="name" class="block text-xs font-semibold uppercase tracking-wide text-slate-500">Full name</label>
                    <div class="relative mt-1.5">
                        <Icon name="user" class="pointer-events-none absolute top-1/2 left-3 h-4 w-4 -translate-y-1/2 text-slate-400" />
                        <input
                            id="name"
                            v-model="form.name"
                            type="text"
                            autocomplete="name"
                            placeholder="Jane Doe"
                            class="block w-full rounded-lg border border-slate-300 py-2.5 pr-3 pl-10 text-sm text-slate-900 placeholder:text-slate-400 focus:border-sky-500 focus:ring-1 focus:ring-sky-500 focus:outline-none"
                        />
                    </div>
                </div>

                <div>
                    <label for="email" class="block text-xs font-semibold uppercase tracking-wide text-slate-500">Email address</label>
                    <div class="relative mt-1.5">
                        <Icon name="envelope" class="pointer-events-none absolute top-1/2 left-3 h-4 w-4 -translate-y-1/2 text-slate-400" />
                        <input
                            id="email"
                            v-model="form.email"
                            type="email"
                            autocomplete="email"
                            placeholder="you@aerealerta.test"
                            class="block w-full rounded-lg border border-slate-300 py-2.5 pr-3 pl-10 text-sm text-slate-900 placeholder:text-slate-400 focus:border-sky-500 focus:ring-1 focus:ring-sky-500 focus:outline-none"
                        />
                    </div>
                </div>

                <div>
                    <label for="password" class="block text-xs font-semibold uppercase tracking-wide text-slate-500">Password</label>
                    <div class="relative mt-1.5">
                        <Icon name="lock" class="pointer-events-none absolute top-1/2 left-3 h-4 w-4 -translate-y-1/2 text-slate-400" />
                        <input
                            id="password"
                            v-model="form.password"
                            :type="showPassword ? 'text' : 'password'"
                            autocomplete="new-password"
                            placeholder="Create a password"
                            class="block w-full rounded-lg border border-slate-300 py-2.5 pr-10 pl-10 text-sm text-slate-900 placeholder:text-slate-400 focus:border-sky-500 focus:ring-1 focus:ring-sky-500 focus:outline-none"
                        />
                        <button
                            type="button"
                            class="absolute inset-y-0 right-0 flex items-center pr-3 text-slate-400 hover:text-slate-600"
                            @click="showPassword = !showPassword"
                        >
                            <span class="sr-only">Toggle password visibility</span>
                            <Icon :name="showPassword ? 'eye-slash' : 'eye'" class="h-5 w-5" />
                        </button>
                    </div>
                </div>

                <div>
                    <label for="password_confirmation" class="block text-xs font-semibold uppercase tracking-wide text-slate-500">Confirm password</label>
                    <div class="relative mt-1.5">
                        <Icon name="lock" class="pointer-events-none absolute top-1/2 left-3 h-4 w-4 -translate-y-1/2 text-slate-400" />
                        <input
                            id="password_confirmation"
                            v-model="form.password_confirmation"
                            :type="showPasswordConfirmation ? 'text' : 'password'"
                            autocomplete="new-password"
                            placeholder="Repeat your password"
                            class="block w-full rounded-lg border border-slate-300 py-2.5 pr-10 pl-10 text-sm text-slate-900 placeholder:text-slate-400 focus:border-sky-500 focus:ring-1 focus:ring-sky-500 focus:outline-none"
                        />
                        <button
                            type="button"
                            class="absolute inset-y-0 right-0 flex items-center pr-3 text-slate-400 hover:text-slate-600"
                            @click="showPasswordConfirmation = !showPasswordConfirmation"
                        >
                            <span class="sr-only">Toggle password visibility</span>
                            <Icon :name="showPasswordConfirmation ? 'eye-slash' : 'eye'" class="h-5 w-5" />
                        </button>
                    </div>
                </div>

                <button
                    type="submit"
                    :disabled="processing"
                    class="flex w-full items-center justify-center gap-2 rounded-lg bg-sky-600 px-4 py-2.5 text-sm font-semibold text-white shadow-sm transition hover:bg-sky-500 disabled:cursor-not-allowed disabled:opacity-70"
                >
                    {{ processing ? 'Creating account…' : 'Create account' }}
                    <span aria-hidden="true">→</span>
                </button>
            </form>

            <p class="mt-6 text-center text-sm text-slate-500">
                Already have an account?
                <Link href="/login" class="font-medium text-sky-600 hover:text-sky-500">Sign in</Link>
            </p>
        </div>
    </div>
</template>
