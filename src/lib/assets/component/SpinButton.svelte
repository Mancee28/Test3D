<script lang="ts">
	import type { ModelViewerElement } from "@google/model-viewer";
	import { handlers } from "svelte/legacy";

    let { viewer } : { viewer : ModelViewerElement } = $props();

    let spin: boolean = $state(false);
    let audio: HTMLAudioElement;
    let hasBeenPlayed: boolean = $state(false);

    function onSpin(){
        if (!viewer) return;
        spin = !spin;
        if (spin) {
        viewer.setAttribute('rotation-per-second', '1080deg');
        if (!hasBeenPlayed){
            audio.currentTime = 14.7;
            hasBeenPlayed = true;
        }
        audio.play();
        } else {
        viewer.removeAttribute('rotation-per-second');
        audio.pause();
        }
    }
</script>

<audio
	bind:this={audio}
	src="/music/rozzi.mp3"
    loop
>
</audio>

<button
    onclick={onSpin}
    aria-pressed={spin}
    class={`inline-flex items-center justify-center rounded-full px-4 py-2 mb-4 text-sm font-medium shadow-sm select-none transition duration-200 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-pink-400/60 ${
        spin
            ? 'bg-zinc-200 text-zinc-900 hover:bg-zinc-300 dark:bg-zinc-700 dark:text-zinc-50 dark:hover:bg-zinc-600'
            : 'bg-pink-500 text-white hover:bg-pink-600 active:bg-pink-700'
    }`}
    >
    {spin ? 'CHILL' : 'SPIN'}
</button>
