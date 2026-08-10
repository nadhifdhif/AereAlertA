<script setup>
import { Link } from '@inertiajs/vue3';

const title = 'AéreAlertA';
</script>

<template>
    <main class="flex min-h-screen items-center justify-center bg-slate-50">
        <div class="text-center">
            <h1 class="text-4xl font-semibold text-slate-900">
                {{ title }}
            </h1>

            <p class="mt-4 text-lg text-slate-500">
                Coming Soon.
            </p>

            <Link
                href="/login"
                class="mt-8 inline-flex items-center justify-center rounded-lg bg-sky-600 px-5 py-2.5 text-sm font-semibold text-white shadow-sm transition hover:bg-sky-500"
            >
                Sign in to preview
            </Link>
        </div>
    </main>
</template>
