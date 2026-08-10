<script setup>
defineProps({
    variant: {
        type: String,
        default: 'light', // 'light' text for dark backgrounds, 'dark' text for light backgrounds
    },
    size: {
        type: String,
        default: 'md', // 'md' | 'lg'
    },
});
</script>

<template>
    <div class="flex items-center gap-2.5">
        <span
            class="flex shrink-0 items-center justify-center rounded-lg bg-gradient-to-br from-sky-400 to-sky-600 shadow-sm"
            :class="size === 'lg' ? 'h-11 w-11' : 'h-9 w-9'"
        >
            <svg viewBox="0 0 24 24" class="h-[55%] w-[55%]">
                <path
                    fill="white"
                    d="M12 2.4c-4.2 3.3-7.3 7.6-7.3 11.4a7.3 7.3 0 0014.5 1.2c.4-2.1-.1-4.5-1.6-7 .5 2.6.1 4.7-1 6.1-.6-3.1-2.2-6.6-4.6-11.7z"
                />
            </svg>
        </span>
        <span
            class="font-semibold tracking-tight"
            :class="[
                variant === 'light' ? 'text-white' : 'text-slate-900',
                size === 'lg' ? 'text-xl' : 'text-lg',
            ]"
        >
            AéreAlertA
        </span>
    </div>
</template>
