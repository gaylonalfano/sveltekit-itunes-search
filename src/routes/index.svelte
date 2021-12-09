<script>
	import { goto } from '$app/navigation';
	let artist = '';
	function search() {
		goto(`${artist}`);
	}

	$: console.log(artist);
</script>

<section>
	<div>
		<div>Search an artist</div>
		<input type="text" bind:value={artist} />
		<button on:click={search}>Search</button>
	</div>
</section>
