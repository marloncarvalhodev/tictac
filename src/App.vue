<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';

const TIMEZONE = 'America/Sao_Paulo';

const timeFormatter = new Intl.DateTimeFormat('pt-BR', {
  timeZone: TIMEZONE,
  hour: '2-digit',
  minute: '2-digit',
  second: '2-digit',
  hour12: false,
});

const weekdayFormatter = new Intl.DateTimeFormat('pt-BR', {
  timeZone: TIMEZONE,
  weekday: 'long',
});

const dateFormatter = new Intl.DateTimeFormat('pt-BR', {
  timeZone: TIMEZONE,
  day: 'numeric',
  month: 'long',
  year: 'numeric',
});

const now = ref(new Date());
let intervalId = null;

const timeParts = computed(() => {
  const parts = timeFormatter.formatToParts(now.value);
  let hour = '00';
  let minute = '00';
  let second = '00';

  for (const part of parts) {
    if (part.type === 'hour') hour = part.value;
    else if (part.type === 'minute') minute = part.value;
    else if (part.type === 'second') second = part.value;
  }

  return { hour, minute, second };
});

const hoursMinutes = computed(() => {
  return `${timeParts.value.hour}:${timeParts.value.minute}`;
});

const seconds = computed(() => {
  return timeParts.value.second;
});

const weekday = computed(() => {
  const raw = weekdayFormatter.format(now.value);
  return raw ? raw.charAt(0).toUpperCase() + raw.slice(1) : '';
});

const formattedDate = computed(() => {
  return dateFormatter.format(now.value);
});

const progressPercentage = computed(() => {
  const currentSec = Number(seconds.value);
  return ((currentSec / 59) * 100).toFixed(2);
});

onMounted(() => {
  now.value = new Date();
  intervalId = setInterval(() => {
    now.value = new Date();
  }, 1000);
});

onUnmounted(() => {
  if (intervalId !== null) {
    clearInterval(intervalId);
    intervalId = null;
  }
});
</script>

<template>
  <div class="min-h-screen bg-[#09090b] flex items-center justify-center overflow-hidden p-6 font-sans antialiased">
    <main
      class="w-full max-w-[440px] bg-[#121215] border border-[#27272a] rounded-lg overflow-hidden flex flex-col"
      aria-label="Relógio Digital - Horário Oficial de Brasília"
    >
      <div class="px-7 py-7 md:px-10 md:py-9 flex flex-col">
        <header class="flex items-center justify-between mb-6 md:mb-7 tracking-widest text-xs font-medium uppercase text-zinc-500 select-none">
          <span>TICTAC</span>
          <span>BRT &bull; UTC-3</span>
        </header>

        <time
          class="flex items-baseline tabular-nums leading-none mb-6 md:mb-7 select-none"
          aria-live="polite"
        >
          <span class="text-zinc-100 font-light text-6xl md:text-7xl tracking-tight">
            {{ hoursMinutes }}
          </span>
          <span class="text-zinc-500 font-light text-3xl md:text-4xl tracking-tight ml-1">
            :{{ seconds }}
          </span>
        </time>

        <footer class="flex items-center">
          <p class="text-sm font-normal leading-relaxed flex flex-wrap items-center gap-2">
            <span class="text-zinc-100">{{ weekday }}</span>
            <span class="text-zinc-700 select-none" aria-hidden="true">/</span>
            <span class="text-zinc-500">{{ formattedDate }}</span>
          </p>
        </footer>
      </div>

      <div
        class="w-full h-[2px] bg-[#27272a] overflow-hidden"
        role="progressbar"
        aria-label="Progresso do minuto atual"
        aria-valuemin="0"
        aria-valuemax="59"
        :aria-valuenow="Number(seconds)"
      >
        <div
          class="h-full bg-zinc-200 transition-[width] duration-200 ease-out"
          :style="{ width: `${progressPercentage}%` }"
        ></div>
      </div>
    </main>
  </div>
</template>
