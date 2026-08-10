<script setup>
import { computed } from 'vue';
import Badge from '@/Components/Badge.vue';

const props = defineProps({
    label: { type: String, required: true },
    value: { type: [String, Number], required: true },
    unit: { type: String, default: '' },
    badgeText: { type: String, default: '' },
    badgeColor: { type: String, default: 'slate' },
    trendLabel: { type: String, default: '' },
    trendDirection: { type: String, default: 'up' }, // 'up' | 'down'
    trendTone: { type: String, default: 'neutral' }, // 'positive' | 'negative' | 'neutral'
    accent: { type: String, default: 'sky' }, // 'sky' | 'emerald' | 'amber' | 'rose'
    points: { type: Array, default: () => [] },
});

const iconBg = {
    sky: 'bg-sky-50 text-sky-600',
    emerald: 'bg-emerald-50 text-emerald-600',
    amber: 'bg-amber-50 text-amber-600',
    rose: 'bg-rose-50 text-rose-600',
};

const strokeColor = {
    sky: 'text-sky-500',
    emerald: 'text-emerald-500',
    amber: 'text-amber-500',
    rose: 'text-rose-500',
};

const trendColor = {
    positive: 'text-emerald-600',
    negative: 'text-rose-600',
    neutral: 'text-slate-500',
};

const sparklinePoints = computed(() => {
    if (!props.points.length) return '';
    const step = 100 / (props.points.length - 1);
    return props.points.map((y, i) => `${i * step},${y}`).join(' ');
});
</script>

<template>
    <div class="rounded-xl border border-slate-200 bg-white p-5 shadow-sm">
        <div class="flex items-start justify-between">
            <span class="flex h-10 w-10 items-center justify-center rounded-lg" :class="iconBg[accent]">
                <span class="h-5 w-5">
                    <slot name="icon" />
                </span>
            </span>
            <Badge v-if="badgeText" :color="badgeColor">{{ badgeText }}</Badge>
        </div>

        <p class="mt-4 text-sm font-medium text-slate-500">{{ label }}</p>
        <p class="mt-1 flex items-baseline gap-1">
            <span class="text-2xl font-semibold text-slate-900">{{ value }}</span>
            <span v-if="unit" class="text-sm font-medium text-slate-400">{{ unit }}</span>
        </p>

        <div class="mt-4 flex items-end justify-between gap-2">
            <p v-if="trendLabel" class="flex items-center gap-1 text-xs font-medium" :class="trendColor[trendTone]">
                <svg v-if="trendDirection === 'up'" viewBox="0 0 12 12" class="h-3 w-3" fill="currentColor">
                    <path d="M6 2l4 5H2l4-5z" />
                </svg>
                <svg v-else viewBox="0 0 12 12" class="h-3 w-3" fill="currentColor">
                    <path d="M6 10L2 5h8l-4 5z" />
                </svg>
                {{ trendLabel }}
            </p>
            <svg v-if="points.length" viewBox="0 0 100 30" preserveAspectRatio="none" class="h-8 w-20 shrink-0">
                <polyline
                    :points="sparklinePoints"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2.5"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    :class="strokeColor[accent]"
                />
            </svg>
        </div>
    </div>
</template>
