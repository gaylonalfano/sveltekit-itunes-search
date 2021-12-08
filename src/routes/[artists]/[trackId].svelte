<script>
	import { page } from '$app/stores';
	import { onMount } from 'svelte';

	let songResults = [];

	onMount(async () => {
		let trackId = $page.params.trackId;
		const response = await fetch(`https://itunes.apple.com/search?term=${trackId}&entity=song`);
		const data = await response.json();

		songResults = data.results[0];
		console.log(songResults);
	});
</script>

<section>
	<div>{$page.params.trackId}</div>
	<h3>{songResults}</h3>
</section>
