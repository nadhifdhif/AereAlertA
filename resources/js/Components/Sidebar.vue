<script setup>
import { computed, ref } from 'vue';
import { Link, router, usePage } from '@inertiajs/vue3';
import AppLogo from '@/Components/AppLogo.vue';
import Icon from '@/Components/Icon.vue';

defineProps({
    open: {
        type: Boolean,
        default: false,
    },
});

defineEmits(['close']);

const page = usePage();
const currentPath = computed(() => page.url.split('?')[0]);

const accountMenuOpen = ref(false);

function logout() {
    accountMenuOpen.value = false;
    router.visit('/login');
}

const navigation = [
    {
        section: 'Overview',
        items: [
            { name: 'Dashboard', href: '/dashboard', icon: 'home' },
            { name: 'Monitoring', href: '#', icon: 'chart', soon: true },
            { name: 'History', href: '#', icon: 'clock', soon: true },
        ],
    },
    {
        section: 'Devices',
        items: [
            { name: 'All Devices', href: '#', icon: 'chip', soon: true },
            { name: 'Device Control', href: '#', icon: 'sliders', soon: true },
            { name: 'Live Camera', href: '#', icon: 'camera', soon: true },
        ],
    },
    {
        section: 'Insights',
        items: [
            { name: 'AI Analysis', href: '#', icon: 'sparkles', soon: true },
            { name: 'Weather', href: '#', icon: 'cloud', soon: true },
            { name: 'Alerts', href: '#', icon: 'bell', soon: true },
        ],
    },
    {
        section: 'Administration',
        items: [
            { name: 'Users', href: '#', icon: 'users', soon: true },
            { name: 'Settings', href: '#', icon: 'settings', soon: true },
        ],
    },
];
</script>

<template>
    <div>
        <!-- Mobile drawer backdrop -->
        <div v-show="open" class="fixed inset-0 z-40 bg-slate-900/60 lg:hidden" @click="$emit('close')" />

        <!-- Account dropdown backdrop. Kept OUTSIDE <aside> on purpose: that element is
             translated (transform), which would turn it into the containing block for any
             `fixed` descendant and shrink this overlay down to the sidebar's own box. -->
        <div v-if="accountMenuOpen" class="fixed inset-0 z-40" @click="accountMenuOpen = false" />

        <!-- Sidebar panel: off-canvas drawer on mobile, always visible on lg+ -->
        <aside
            class="fixed inset-y-0 left-0 z-50 flex w-72 transform flex-col bg-slate-900 transition-transform duration-300 ease-in-out lg:translate-x-0"
            :class="open ? 'translate-x-0' : '-translate-x-full'"
        >
            <div class="flex h-16 shrink-0 items-center justify-between px-5">
                <AppLogo />
                <button type="button" class="text-slate-400 hover:text-white lg:hidden" @click="$emit('close')">
                    <span class="sr-only">Close sidebar</span>
                    <Icon name="xmark" class="h-6 w-6" />
                </button>
            </div>

            <nav
                class="flex-1 space-y-5 overflow-y-auto px-4 pb-4 [scrollbar-color:rgb(51_65_85)_transparent] [scrollbar-width:thin] [&::-webkit-scrollbar]:w-1.5 [&::-webkit-scrollbar-thumb]:rounded-full [&::-webkit-scrollbar-thumb]:bg-slate-700 [&::-webkit-scrollbar-track]:bg-transparent"
            >
                <div v-for="group in navigation" :key="group.section">
                    <p class="px-2.5 text-xs font-semibold uppercase tracking-wider text-slate-500">
                        {{ group.section }}
                    </p>
                    <ul class="mt-1.5 space-y-0.5">
                        <li v-for="item in group.items" :key="item.name">
                            <component
                                :is="item.soon ? 'div' : Link"
                                :href="item.soon ? undefined : item.href"
                                class="flex items-center justify-between rounded-lg px-2.5 py-1.5 text-sm font-medium transition"
                                :class="item.soon
                                    ? 'cursor-default text-slate-500'
                                    : currentPath === item.href
                                        ? 'bg-sky-600 text-white'
                                        : 'text-slate-300 hover:bg-slate-800 hover:text-white'"
                            >
                                <span class="flex items-center gap-3">
                                    <Icon :name="item.icon" class="h-5 w-5 shrink-0" />
                                    {{ item.name }}
                                </span>
                                <span
                                    v-if="item.soon"
                                    class="rounded-full bg-slate-800 px-1.5 py-0.5 text-[10px] font-semibold uppercase tracking-wide text-slate-500"
                                >
                                    Soon
                                </span>
                            </component>
                        </li>
                    </ul>
                </div>
            </nav>

            <!-- Account -->
            <div class="relative shrink-0 border-t border-slate-800 p-3">
                <button
                    type="button"
                    class="flex w-full items-center gap-2.5 rounded-lg px-2 py-2 text-left hover:bg-slate-800"
                    @click="accountMenuOpen = !accountMenuOpen"
                >
                    <span class="flex h-8 w-8 shrink-0 items-center justify-center rounded-full bg-sky-600 text-xs font-semibold text-white">
                        AU
                    </span>
                    <span class="min-w-0 flex-1">
                        <span class="block truncate text-sm font-medium text-white">Admin User</span>
                        <span class="block truncate text-xs text-slate-400">Administrator</span>
                    </span>
                    <Icon name="chevron-down" class="h-4 w-4 shrink-0 text-slate-500" />
                </button>

                <div
                    v-if="accountMenuOpen"
                    class="absolute inset-x-3 bottom-full z-50 mb-2 rounded-xl border border-slate-800 bg-slate-900 py-1.5 shadow-lg"
                >
                    <div class="px-3 py-2">
                        <p class="text-sm font-medium text-white">Admin User</p>
                        <p class="text-xs text-slate-400">admin@aerealerta.test</p>
                    </div>
                    <div class="my-1 h-px bg-slate-800" />
                    <p class="flex cursor-default items-center gap-2 px-3 py-2 text-sm text-slate-500">
                        <Icon name="settings" class="h-4 w-4" />
                        Settings
                        <span class="ml-auto rounded-full bg-slate-800 px-1.5 py-0.5 text-[10px] font-semibold uppercase text-slate-500">Soon</span>
                    </p>
                    <button
                        type="button"
                        class="flex w-full items-center gap-2 px-3 py-2 text-left text-sm text-slate-300 hover:bg-slate-800"
                        @click="logout"
                    >
                        <Icon name="logout" class="h-4 w-4" />
                        Sign out
                    </button>
                </div>
            </div>
        </aside>
    </div>
</template>
