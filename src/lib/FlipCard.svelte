<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	
	export let buttons = []
	
	let flipped, data
	
	function flip(e) {
		if (!flipped) {
			const clicked = e.target.innerHTML
			data = clicked
			
			dispatch('like', {
				data
			});
		}
		flipped = !flipped
	}
</script>

<div class="card">
  <div class:flipped class="inner">
		<div class="front">
			{#each buttons as button}
				<button aria-label={button} on:click={flip}>{ button.toUpperCase() }</button>
			{/each}
		</div>
		<div class="back">
			Great! We like {data} too.
		</div>
	</div>
</div>

<style>
.card {
  background-color: transparent;
  width: 300px;
  height: 200px;
  perspective: 1000px;
	margin: 1rem
}
.inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}
.flipped {
  transform: rotateY(180deg);
}
	.front, .back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
	display: flex;
	align-items: center;
	justify-content: center;
	gap: .5rem;
}
	.front {
  background-color: #bbb;
  color: black;
}
	
.back {
  background-color: dodgerblue;
  color: white;
  transform: rotateY(180deg);
	flex-direction: column;
}
</style>