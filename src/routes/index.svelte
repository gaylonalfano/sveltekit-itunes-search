<script>
	import { goto } from '$app/navigation';
	let artists = '';
	function search() {
		goto(`${artists}`);
	}

	$: console.log(artists);
</script>

<section>
	<div>
		<div>Search an artist</div>
		<input type="text" bind:value={artists} />
		<button on:click={search}>Search</button>
	</div>
</section>
