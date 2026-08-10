<script setup>
import { ref } from 'vue';
import { Head } from '@inertiajs/vue3';
import Sidebar from '@/Components/Sidebar.vue';
import Icon from '@/Components/Icon.vue';

defineProps({
    title: {
        type: String,
        default: 'Dashboard',
    },
});

const sidebarOpen = ref(false);
const notificationsOpen = ref(false);

const notifications = [
    { id: 1, message: 'Gas level (MQ-2) exceeded threshold in Server Room', time: '2m ago', tone: 'rose' },
    { id: 2, message: 'Humidity above optimal range in Greenhouse Zone A', time: '18m ago', tone: 'amber' },
    { id: 3, message: 'New device "DHT22 Node 5" registered', time: '3h ago', tone: 'sky' },
];
</script>

<template>
    <Head :title="title" />

    <div class="min-h-screen bg-slate-50">
        <Sidebar :open="sidebarOpen" @close="sidebarOpen = false" />

        <div class="lg:pl-72">
            <header class="sticky top-0 z-30 flex h-16 items-center gap-4 border-b border-slate-200 bg-white/80 px-4 backdrop-blur sm:px-6 lg:px-8">
                <button type="button" class="text-slate-500 hover:text-slate-700 lg:hidden" @click="sidebarOpen = true">
                    <span class="sr-only">Open sidebar</span>
                    <Icon name="bars3" class="h-6 w-6" />
                </button>

                <div class="relative max-w-md flex-1">
                    <Icon name="search" class="pointer-events-none absolute left-3 top-1/2 h-4 w-4 -translate-y-1/2 text-slate-400" />
                    <input
                        type="text"
                        placeholder="Search devices, alerts..."
                        class="w-full rounded-lg border border-slate-200 bg-slate-50 py-2 pl-9 pr-3 text-sm text-slate-700 placeholder:text-slate-400 focus:border-sky-500 focus:bg-white focus:outline-none focus:ring-1 focus:ring-sky-500"
                    />
                </div>

                <div class="flex items-center gap-2 sm:gap-4">
                    <!-- Notifications -->
                    <div class="relative">
                        <button
                            type="button"
                            class="relative rounded-full p-2 text-slate-500 hover:bg-slate-100 hover:text-slate-700"
                            @click="notificationsOpen = !notificationsOpen"
                        >
                            <span class="sr-only">View notifications</span>
                            <Icon name="bell" class="h-6 w-6" />
                            <span class="absolute right-1.5 top-1.5 h-2 w-2 rounded-full bg-rose-500 ring-2 ring-white" />
                        </button>

                        <div v-if="notificationsOpen" class="fixed inset-0 z-30" @click="notificationsOpen = false" />

                        <div
                            v-if="notificationsOpen"
                            class="absolute right-0 z-40 mt-2 w-80 origin-top-right rounded-xl border border-slate-200 bg-white py-2 shadow-lg"
                        >
                            <p class="px-4 py-1.5 text-xs font-semibold uppercase tracking-wide text-slate-400">Notifications</p>
                            <div v-for="n in notifications" :key="n.id" class="flex gap-3 px-4 py-2.5 hover:bg-slate-50">
                                <span
                                    class="mt-1.5 h-1.5 w-1.5 shrink-0 rounded-full"
                                    :class="{
                                        'bg-rose-500': n.tone === 'rose',
                                        'bg-amber-500': n.tone === 'amber',
                                        'bg-sky-500': n.tone === 'sky',
                                    }"
                                />
                                <div>
                                    <p class="text-sm text-slate-700">{{ n.message }}</p>
                                    <p class="mt-0.5 text-xs text-slate-400">{{ n.time }}</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </header>

            <main class="px-4 py-8 sm:px-6 lg:px-8">
                <slot />
            </main>
        </div>
    </div>
</template>
