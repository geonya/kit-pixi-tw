<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import * as PIXI from 'pixi.js';
	let elemCanvas: HTMLCanvasElement;
	let app: PIXI.Application;
	onMount(() => {
		PIXI.settings.SCALE_MODE = PIXI.SCALE_MODES.NEAREST;
		app = new PIXI.Application({
			view: elemCanvas,
			resizeTo: document.body,
			backgroundColor: 0x141414
		});
		if (app === null) return;

		let sprite = PIXI.Sprite.from('sample.png');
		app.stage.addChild(sprite);
		// Add a variable to count up the seconds our demo has been running
		let elapsed = 0.0;
		// Tell our application's ticker to run a new callback every frame, passing
		// in the amount of time that has passed since the last tick
		app.ticker.add((delta) => {
			// Add the time to our total elapsed time
			elapsed += delta;
			// Update the sprite's X position based on the cosine of our elapsed time.  We divide
			// by 50 to slow the animation down a bit...
			sprite.x = 100.0 + Math.cos(elapsed / 10.0) * 100.0;
		});
	});
	onDestroy(() => {
		if (app !== undefined) app.stop();
	});
</script>

<canvas id="app" bind:this={elemCanvas} />
