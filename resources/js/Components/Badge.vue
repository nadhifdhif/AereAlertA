<script setup>
defineProps({
    color: {
        type: String,
        default: 'slate', // 'emerald' | 'amber' | 'rose' | 'sky' | 'slate'
    },
});

const styles = {
    emerald: 'bg-emerald-50 text-emerald-700 ring-emerald-600/20',
    amber: 'bg-amber-50 text-amber-800 ring-amber-600/20',
    rose: 'bg-rose-50 text-rose-700 ring-rose-600/20',
    sky: 'bg-sky-50 text-sky-700 ring-sky-600/20',
    slate: 'bg-slate-100 text-slate-600 ring-slate-500/10',
};

const dots = {
    emerald: 'bg-emerald-500',
    amber: 'bg-amber-500',
    rose: 'bg-rose-500',
    sky: 'bg-sky-500',
    slate: 'bg-slate-400',
};
</script>

<template>
    <span
        class="inline-flex w-fit items-center gap-1.5 rounded-full px-2.5 py-0.5 text-xs font-medium ring-1 ring-inset"
        :class="styles[color] ?? styles.slate"
    >
        <span class="h-1.5 w-1.5 rounded-full" :class="dots[color] ?? dots.slate" />
        <slot />
    </span>
</template>
