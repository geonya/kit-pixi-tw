<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import * as PIXI from 'pixi.js';

	let elemCanvas: HTMLCanvasElement;
	let canvas: PIXI.Application;
	onMount(() => {
		PIXI.settings.SCALE_MODE = PIXI.SCALE_MODES.NEAREST;

		canvas = new PIXI.Application({
			view: elemCanvas,
			resizeTo: document.body,
			backgroundColor: 0x141414
		});
		if (canvas === null) return;
	});
	onDestroy(() => {
		if (canvas !== undefined) canvas.stop();
	});
</script>

<canvas id="canvas" bind:this={elemCanvas} />
