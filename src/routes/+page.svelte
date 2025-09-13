<script lang="ts">
import type { ModelViewerElement } from '@google/model-viewer';
  import { onMount } from 'svelte';

  let ModelViewerReady = $state(false);
  // svelte-ignore non_reactive_update
  let viewer: ModelViewerElement;

  onMount(async () => {
    await import('@google/model-viewer');
    ModelViewerReady = true;
  });

</script>

<section class="min-h-screen bg-gradient-to-b from-rose-50 via-white to-white dark:from-neutral-900 dark:via-neutral-950 dark:to-black text-neutral-800 dark:text-neutral-100">
  <div class="mx-auto max-w-6xl px-6 py-10 lg:py-14">
    <header class="mb-8 lg:mb-10 fade-in">
      <div class="inline-flex items-center gap-2 rounded-full bg-rose-100/70 px-3 py-1 text-sm font-medium text-rose-700 ring-1 ring-rose-200 dark:bg-rose-400/10 dark:text-rose-300 dark:ring-rose-400/20">
        <span>Modello 3D</span>
        <span>•</span>
        <span>Ciambella con glassa rosa</span>
      </div>
      <h1 class="mt-4 text-3xl font-semibold tracking-tight sm:text-4xl lg:text-5xl">
        Una ciambella così bella che viene voglia di morderla
      </h1>
    </header>

    <!-- Model Card -->
    <div class="relative isolate">
      <!-- Decorative glow -->
      <div class="pointer-events-none absolute inset-0 -z-10 opacity-70">
        <div class="donut-glow h-full w-full"></div>
      </div>

      <div class="relative overflow-hidden rounded-2xl bg-white/70 p-2 ring-1 ring-black/5 backdrop-blur-md shadow-xl dark:bg-white/5 dark:ring-white/10">
        {#if ModelViewerReady}
          <div class="relative">
            <model-viewer
              bind:this={viewer}
              src="/models/donut.glb"
              alt="Ciambella 3D con glassa rosa"
              camera-controls
              interaction-prompt="auto"
              reveal="auto"
              loading="eager"
              preload
              dpr="1 2"
              tone-mapping="aces"
              environment-image="neutral"
              exposure=1.1
              shadow-intensity=0.9
              shadow-softness=0.9
              ar
              ar-modes="webxr scene-viewer quick-look"
              style="width:100%; height:520px; border-radius:1rem;"
            ></model-viewer>
          </div>
        {:else}
          <!-- Skeleton while loading model-viewer definition -->
          <div class="grid h-[520px] w-full place-items-center rounded-xl bg-gradient-to-br from-rose-100/60 via-white to-rose-50/60 dark:from-neutral-800 dark:via-neutral-900 dark:to-neutral-800">
            <div class="h-24 w-24 animate-spin rounded-full border-4 border-rose-300 border-t-rose-600 dark:border-neutral-600 dark:border-t-neutral-300"></div>
          </div>
        {/if}
      </div>
    </div>

    <footer class="mt-8 flex flex-wrap items-center justify-between gap-4 text-sm text-neutral-500 dark:text-neutral-400">
      <p>
        Suggerimento: trascina per ruotare, usa <kbd class="rounded border border-neutral-300 px-1 text-neutral-700 dark:border-neutral-600 dark:text-neutral-200">⌘/Ctrl</kbd> + rotella per zoom.
      </p>
      <a href="/models/donut.glb" download class="inline-flex items-center gap-2 rounded-full bg-white/70 px-3 py-1 ring-1 ring-black/5 backdrop-blur transition hover:bg-white/90 dark:bg-white/5 dark:ring-white/10">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><path d="M7 10l5 5 5-5"/><path d="M12 15V3"/></svg>
        Scarica modello (.glb)
      </a>
    </footer>
  </div>
</section>