<script>
	import { spring } from 'svelte/motion';
	import { pannable } from './pannable.js';

	const coords = spring(
		{ x: 0, y: 0 },
		{
			stiffness: 0.2,
			damping: 0.4
		}
	);

	function handlePanStart() {
		coords.stiffness = coords.damping = 1;
	}

	function handlePanMove(event) {
		coords.update(($coords) => ({
			x: $coords.x + event.detail.dx,
			y: $coords.y + event.detail.dy
		}));
	}

	function handlePanEnd(event) {
		coords.stiffness = 0.2;
		coords.damping = 0.4;
		coords.set({ x: 0, y: 0 });
	}
</script>

<div
	class="box"
	use:pannable
	on:panstart={handlePanStart}
	on:panmove={handlePanMove}
	on:panend={handlePanEnd}
	style="transform:
		translate({$coords.x}px,{$coords.y}px)
		rotate({$coords.x * 0.2}deg)"
/>

<style>
    .box {
        --width: 30%;
        --height: 30%;
        position: inherit;
		width: 33%;
		height: 33%;
        border-radius: 4px;
        background-image: url('../images/logoN.png');
        background-size: cover;
        cursor: move;
    }
</style>