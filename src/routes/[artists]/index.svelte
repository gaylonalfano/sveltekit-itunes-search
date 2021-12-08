<script context="module">
	export async function load({ page, fetch, session, stuff }) {
		// load() runs before rendering the content of the page
		// Want to make a fetch() to the API using pokemon id, which
		// is available from page.params object
		const searchedArtist = page.params.artists;
		const response = await fetch(
			`https://itunes.apple.com/search?term=${searchedArtist}&entity=song`
		);
		const data = await response.json();
		const songs = data.results;
		console.log(songs);

		// Now return Object with props property and add our pokeman data
		// NOTE Again, this all runs BEFORE Svelte renders anything!
		return { props: { songs } };
	}
</script>

<script>
	import { goto } from '$app/navigation';
	import { page } from '$app/stores';

	export let songs;

	// import { onMount } from 'svelte';

	// let songResults = [];

	// onMount(async () => {
	// 	let artist = $page.params.searchText;
	// 	console.log('artist: ', artist);
	// 	console.log('params.searchText: ', $page.params.searchText);

	// 	songResults = data.results;
	// 	// console.log(songResults);
	// });
</script>

<section>
	<div>{$page.params.artists}</div>
	{#each songs as song, i}
		<h3>{song.artistName}</h3>
		<p>{song.trackId}</p>
	{/each}
</section>
