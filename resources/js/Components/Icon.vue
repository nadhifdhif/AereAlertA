<script setup>
defineProps({
    name: {
        type: String,
        required: true,
    },
});
</script>

<template>
    <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="1.75"
        aria-hidden="true"
    >
        <template v-if="name === 'home'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 12l8.954-8.955a1.125 1.125 0 011.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25" />
        </template>

        <template v-else-if="name === 'chart'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3 13.125C3 12.504 3.504 12 4.125 12h2.25c.621 0 1.125.504 1.125 1.125v6.75C7.5 20.496 6.996 21 6.375 21h-2.25A1.125 1.125 0 013 19.875v-6.75zM9.75 8.625c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125v11.25c0 .621-.504 1.125-1.125 1.125h-2.25a1.125 1.125 0 01-1.125-1.125V8.625zM16.5 4.125c0-.621.504-1.125 1.125-1.125h2.25C20.496 3 21 3.504 21 4.125v15.75c0 .621-.504 1.125-1.125 1.125h-2.25a1.125 1.125 0 01-1.125-1.125V4.125z" />
        </template>

        <template v-else-if="name === 'clock'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v6h4.5m4.5 0a9 9 0 11-18 0 9 9 0 0118 0z" />
        </template>

        <template v-else-if="name === 'chip'">
            <rect x="7" y="7" width="10" height="10" rx="1.5" stroke-linecap="round" stroke-linejoin="round" />
            <path stroke-linecap="round" d="M9 3.5V7M12 3.5V7M15 3.5V7M9 17v3.5M12 17v3.5M15 17v3.5M3.5 9H7M3.5 12H7M3.5 15H7M17 9h3.5M17 12h3.5M17 15h3.5" />
        </template>

        <template v-else-if="name === 'sliders'">
            <path stroke-linecap="round" d="M6 4.5v15M12 4.5v15M18 4.5v15" />
            <circle cx="6" cy="14" r="1.75" />
            <circle cx="12" cy="8" r="1.75" />
            <circle cx="18" cy="17" r="1.75" />
        </template>

        <template v-else-if="name === 'camera'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M4 8.5a1.5 1.5 0 011.5-1.5h2l1-1.5h7l1 1.5h2A1.5 1.5 0 0120 8.5v9a1.5 1.5 0 01-1.5 1.5h-13A1.5 1.5 0 014 17.5v-9z" />
            <circle cx="12" cy="13" r="3.25" />
        </template>

        <template v-else-if="name === 'sparkles'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 3l1.8 5.2L19 10l-5.2 1.8L12 17l-1.8-5.2L5 10l5.2-1.8L12 3z" />
            <path stroke-linecap="round" stroke-linejoin="round" d="M18.5 15l.7 2 2 .7-2 .7-.7 2-.7-2-2-.7 2-.7.7-2z" />
        </template>

        <template v-else-if="name === 'cloud'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M7 18a4 4 0 110-8 5 5 0 019.58-1.5A4 4 0 1118 18H7z" />
        </template>

        <template v-else-if="name === 'bell'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 3a4 4 0 00-4 4v2.5c0 1.5-.6 2.9-1.7 4L5 15h14l-1.3-1.5c-1.1-1.1-1.7-2.5-1.7-4V7a4 4 0 00-4-4z" />
            <path stroke-linecap="round" stroke-linejoin="round" d="M9.5 18a2.5 2.5 0 005 0" />
        </template>

        <template v-else-if="name === 'users'">
            <circle cx="9" cy="8" r="3" />
            <path stroke-linecap="round" stroke-linejoin="round" d="M3.5 19c0-3.04 2.46-5.5 5.5-5.5s5.5 2.46 5.5 5.5" />
            <circle cx="17" cy="9" r="2.25" />
            <path stroke-linecap="round" stroke-linejoin="round" d="M15.5 19c0-2.2.9-4.1 3.2-4.7.8.5 1.8 1.5 1.8 3.2" />
        </template>

        <template v-else-if="name === 'settings'">
            <circle cx="12" cy="12" r="3.25" />
            <circle cx="12" cy="12" r="7.5" />
            <g fill="currentColor" stroke="none">
                <rect x="10.9" y="2.75" width="2.2" height="3" rx="0.6" />
                <rect x="10.9" y="2.75" width="2.2" height="3" rx="0.6" transform="rotate(60 12 12)" />
                <rect x="10.9" y="2.75" width="2.2" height="3" rx="0.6" transform="rotate(120 12 12)" />
                <rect x="10.9" y="2.75" width="2.2" height="3" rx="0.6" transform="rotate(180 12 12)" />
                <rect x="10.9" y="2.75" width="2.2" height="3" rx="0.6" transform="rotate(240 12 12)" />
                <rect x="10.9" y="2.75" width="2.2" height="3" rx="0.6" transform="rotate(300 12 12)" />
            </g>
        </template>

        <template v-else-if="name === 'bars3'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5M3.75 17.25h16.5" />
        </template>

        <template v-else-if="name === 'xmark'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
        </template>

        <template v-else-if="name === 'eye'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z" />
            <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
        </template>

        <template v-else-if="name === 'eye-slash'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3.98 8.223A10.477 10.477 0 001.934 12C3.226 16.338 7.244 19.5 12 19.5c.993 0 1.953-.138 2.863-.395M6.228 6.228A10.45 10.45 0 0112 4.5c4.756 0 8.773 3.162 10.065 7.498a10.523 10.523 0 01-4.293 5.774M6.228 6.228L3 3m3.228 3.228l3.65 3.65m7.894 7.894L21 21m-3.228-3.228l-3.65-3.65m0 0a3 3 0 10-4.243-4.243m4.242 4.242L9.88 9.88" />
        </template>

        <template v-else-if="name === 'logout'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 9V5.25A2.25 2.25 0 0013.5 3h-6a2.25 2.25 0 00-2.25 2.25v13.5A2.25 2.25 0 007.5 21h6a2.25 2.25 0 002.25-2.25V15M12 9l-3 3m0 0l3 3m-3-3h12.75" />
        </template>

        <template v-else-if="name === 'search'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
        </template>

        <template v-else-if="name === 'chevron-down'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
        </template>

        <template v-else-if="name === 'thermometer'">
            <rect x="10.5" y="3" width="3" height="13" rx="1.5" stroke-linecap="round" stroke-linejoin="round" />
            <circle cx="12" cy="17.5" r="3.25" />
        </template>

        <template v-else-if="name === 'droplet'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 3.5c3 4 6 8.2 6 11.5a6 6 0 11-12 0c0-3.3 3-7.5 6-11.5z" />
        </template>

        <template v-else-if="name === 'wind'">
            <path stroke-linecap="round" d="M3 8h11.5a2.5 2.5 0 10-2.5-2.5" />
            <path stroke-linecap="round" d="M3 12.5h15a2.5 2.5 0 11-2.5 2.5" />
            <path stroke-linecap="round" d="M3 17h9a2 2 0 102-2" />
        </template>

        <template v-else-if="name === 'flame'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 3c1.5 2.5-1 4-1 6.5a2.5 2.5 0 005 0c0-1-.3-1.8-.8-2.6C17 8.5 18 11 18 13.5a6 6 0 11-12 0C6 9 8.5 6 12 3z" />
        </template>

        <template v-else-if="name === 'envelope'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M21.75 6.75v10.5a2.25 2.25 0 01-2.25 2.25h-15a2.25 2.25 0 01-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25m19.5 0v.243a2.25 2.25 0 01-1.07 1.916l-7.5 4.615a2.25 2.25 0 01-2.36 0L3.32 8.91a2.25 2.25 0 01-1.07-1.916V6.75" />
        </template>

        <template v-else-if="name === 'lock'">
            <path stroke-linecap="round" stroke-linejoin="round" d="M16.5 10.5V6.75a4.5 4.5 0 10-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 002.25-2.25v-6.75a2.25 2.25 0 00-2.25-2.25H6.75a2.25 2.25 0 00-2.25 2.25v6.75a2.25 2.25 0 002.25 2.25z" />
        </template>

        <template v-else-if="name === 'user'">
            <circle cx="12" cy="8" r="3.25" />
            <path stroke-linecap="round" stroke-linejoin="round" d="M4.5 19.5c0-3.6 3.36-6.5 7.5-6.5s7.5 2.9 7.5 6.5" />
        </template>
    </svg>
</template>
