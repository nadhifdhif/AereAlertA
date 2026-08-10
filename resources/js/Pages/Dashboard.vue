<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import StatCard from '@/Components/StatCard.vue';
import Badge from '@/Components/Badge.vue';
import Icon from '@/Components/Icon.vue';

const stats = [
    {
        label: 'Temperature',
        value: '26.4',
        unit: '°C',
        icon: 'thermometer',
        accent: 'sky',
        badgeText: 'Normal',
        badgeColor: 'emerald',
        trendLabel: '+0.8° vs yesterday',
        trendDirection: 'up',
        trendTone: 'neutral',
        points: [20, 17, 19, 13, 15, 9],
    },
    {
        label: 'Humidity',
        value: '58',
        unit: '%RH',
        icon: 'droplet',
        accent: 'sky',
        badgeText: 'Normal',
        badgeColor: 'emerald',
        trendLabel: '-3% vs yesterday',
        trendDirection: 'down',
        trendTone: 'neutral',
        points: [8, 12, 10, 16, 14, 19],
    },
    {
        label: 'Air Quality',
        value: '58',
        unit: 'ppm CO₂eq',
        icon: 'wind',
        accent: 'emerald',
        badgeText: 'Good',
        badgeColor: 'emerald',
        trendLabel: '-4% vs yesterday',
        trendDirection: 'down',
        trendTone: 'positive',
        points: [16, 15, 17, 13, 14, 11],
    },
    {
        label: 'Gas Level',
        value: '112',
        unit: 'ppm',
        icon: 'flame',
        accent: 'amber',
        badgeText: 'Elevated',
        badgeColor: 'amber',
        trendLabel: '+12% vs yesterday',
        trendDirection: 'up',
        trendTone: 'negative',
        points: [22, 19, 21, 15, 17, 10],
    },
];

const trend = {
    labels: ['00:00', '03:00', '06:00', '09:00', '12:00', '15:00', '18:00', '21:00'],
    linePoints: '0,132 86,146 171,153 257,93 343,45 429,34 514,63 600,105',
    areaPath: 'M0,132 L86,146 L171,153 L257,93 L343,45 L429,34 L514,63 L600,105 L600,180 L0,180 Z',
    dots: [
        [0, 132], [86, 146], [171, 153], [257, 93], [343, 45], [429, 34], [514, 63], [600, 105],
    ],
};

const alerts = [
    { id: 1, tone: 'rose', message: 'Gas level (MQ-2) exceeded threshold in Server Room', time: '2 minutes ago' },
    { id: 2, tone: 'amber', message: 'Humidity above optimal range in Greenhouse Zone A', time: '18 minutes ago' },
    { id: 3, tone: 'emerald', message: 'Air quality normalized in Lab 2', time: '1 hour ago' },
    { id: 4, tone: 'sky', message: 'New device "DHT22 Node 5" registered', time: '3 hours ago' },
];

const alertDot = {
    rose: 'bg-rose-500',
    amber: 'bg-amber-500',
    emerald: 'bg-emerald-500',
    sky: 'bg-sky-500',
};

const devices = [
    { id: 1, name: 'DHT22 Node 1', type: 'Temp & Humidity', location: 'Server Room', status: 'Online', statusColor: 'emerald', lastSeen: 'Just now' },
    { id: 2, name: 'DHT22 Node 2', type: 'Temp & Humidity', location: 'Greenhouse A', status: 'Online', statusColor: 'emerald', lastSeen: 'Just now' },
    { id: 3, name: 'MQ-2 Sensor', type: 'Gas & Smoke', location: 'Server Room', status: 'Warning', statusColor: 'amber', lastSeen: '1 min ago' },
    { id: 4, name: 'MQ-135 Sensor', type: 'Air Quality', location: 'Lab 2', status: 'Online', statusColor: 'emerald', lastSeen: '5 min ago' },
    { id: 5, name: 'Camera Unit 1', type: 'Live Camera', location: 'Entrance', status: 'Offline', statusColor: 'rose', lastSeen: '2 hours ago' },
];
</script>

<template>
    <AuthenticatedLayout title="Dashboard">
        <div class="mx-auto max-w-7xl space-y-6">
            <!-- Page header -->
            <div class="flex flex-col gap-2 sm:flex-row sm:items-center sm:justify-between">
                <div>
                    <h1 class="text-2xl font-semibold text-slate-900">Dashboard</h1>
                    <p class="mt-1 text-sm text-slate-500">Real-time overview of your environmental sensors</p>
                </div>
                <span class="inline-flex w-fit items-center gap-1.5 rounded-full bg-amber-50 px-3 py-1 text-xs font-medium text-amber-800 ring-1 ring-amber-600/20 ring-inset">
                    <span class="h-1.5 w-1.5 rounded-full bg-amber-500" />
                    2 alerts need attention
                </span>
            </div>

            <!-- Stat cards -->
            <div class="grid grid-cols-1 gap-5 sm:grid-cols-2 lg:grid-cols-4">
                <StatCard
                    v-for="s in stats"
                    :key="s.label"
                    :label="s.label"
                    :value="s.value"
                    :unit="s.unit"
                    :accent="s.accent"
                    :badge-text="s.badgeText"
                    :badge-color="s.badgeColor"
                    :trend-label="s.trendLabel"
                    :trend-direction="s.trendDirection"
                    :trend-tone="s.trendTone"
                    :points="s.points"
                >
                    <template #icon>
                        <Icon :name="s.icon" class="h-5 w-5" />
                    </template>
                </StatCard>
            </div>

            <!-- Trend chart + alerts -->
            <div class="grid grid-cols-1 gap-5 lg:grid-cols-3">
                <div class="rounded-xl border border-slate-200 bg-white p-6 lg:col-span-2">
                    <div class="flex items-center justify-between">
                        <div>
                            <h2 class="text-sm font-semibold text-slate-900">Temperature Trend</h2>
                            <p class="text-xs text-slate-500">Last 24 hours · Server Room</p>
                        </div>
                        <Badge color="sky">DHT22 Node 1</Badge>
                    </div>

                    <svg viewBox="0 0 600 200" class="mt-4 h-56 w-full" preserveAspectRatio="none">
                        <defs>
                            <linearGradient id="trendFill" x1="0" y1="0" x2="0" y2="1">
                                <stop offset="0%" stop-color="currentColor" stop-opacity="0.28" class="text-sky-500" />
                                <stop offset="100%" stop-color="currentColor" stop-opacity="0" class="text-sky-500" />
                            </linearGradient>
                        </defs>

                        <line v-for="y in [60, 110, 160]" :key="y" x1="0" :y1="y" x2="600" :y2="y" class="stroke-slate-100" stroke-width="1" stroke-dasharray="4 4" />

                        <path :d="trend.areaPath" fill="url(#trendFill)" />
                        <polyline :points="trend.linePoints" fill="none" class="stroke-sky-600" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" />
                        <circle v-for="(d, i) in trend.dots" :key="i" :cx="d[0]" :cy="d[1]" r="4" fill="white" class="stroke-sky-600" stroke-width="2" />
                    </svg>

                    <div class="mt-2 flex justify-between text-[11px] text-slate-400">
                        <span v-for="l in trend.labels" :key="l">{{ l }}</span>
                    </div>
                </div>

                <div class="rounded-xl border border-slate-200 bg-white p-6">
                    <div class="flex items-center justify-between">
                        <h2 class="text-sm font-semibold text-slate-900">Recent Alerts</h2>
                        <span class="cursor-default text-xs font-medium text-slate-400">View all</span>
                    </div>

                    <ul class="mt-4 space-y-4">
                        <li v-for="a in alerts" :key="a.id" class="flex gap-3">
                            <span class="mt-1.5 h-1.5 w-1.5 shrink-0 rounded-full" :class="alertDot[a.tone]" />
                            <div>
                                <p class="text-sm leading-snug text-slate-700">{{ a.message }}</p>
                                <p class="mt-0.5 text-xs text-slate-400">{{ a.time }}</p>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>

            <!-- Devices table -->
            <div class="overflow-hidden rounded-xl border border-slate-200 bg-white">
                <div class="flex items-center justify-between border-b border-slate-100 px-6 py-4">
                    <div>
                        <h2 class="text-sm font-semibold text-slate-900">Devices</h2>
                        <p class="text-xs text-slate-500">4 of 5 devices online</p>
                    </div>
                    <span class="cursor-default text-xs font-medium text-slate-400">Manage devices</span>
                </div>

                <div class="overflow-x-auto">
                    <table class="w-full text-left text-sm">
                        <thead>
                            <tr class="text-xs uppercase tracking-wide text-slate-400">
                                <th class="px-6 py-3 font-medium">Device</th>
                                <th class="px-6 py-3 font-medium">Type</th>
                                <th class="px-6 py-3 font-medium">Location</th>
                                <th class="px-6 py-3 font-medium">Status</th>
                                <th class="px-6 py-3 font-medium">Last seen</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100">
                            <tr v-for="d in devices" :key="d.id" class="hover:bg-slate-50">
                                <td class="px-6 py-3 font-medium text-slate-800">{{ d.name }}</td>
                                <td class="px-6 py-3 text-slate-500">{{ d.type }}</td>
                                <td class="px-6 py-3 text-slate-500">{{ d.location }}</td>
                                <td class="px-6 py-3">
                                    <Badge :color="d.statusColor">{{ d.status }}</Badge>
                                </td>
                                <td class="px-6 py-3 text-slate-500">{{ d.lastSeen }}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
