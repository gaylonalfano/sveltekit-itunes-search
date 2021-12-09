<script context="module">
	export async function load({ page, fetch, session, stuff }) {
		// load() runs before rendering the content of the page
		// Want to make a fetch() to the API using page.params
		const searchedArtist = page.params.artist;
		const response = await fetch(
			`https://itunes.apple.com/search?term=${searchedArtist}&entity=song`
		);
		const data = await response.json();
		const songs = data.results;
		console.log(songs);

		// Now return Object with props property and add our pokeman data
		// NOTE Again, this all runs BEFORE Svelte renders anything!
		return {
			props: {
				artist: searchedArtist,
				songs
			}
		};
	}
</script>

<script>
	import { goto } from '$app/navigation';

	// NOTE Must use export!
	export let songs;
	export let artist;
</script>

<section>
	<div>{artist}</div>
	<ul>
		{#each songs as song, i}
			<li>
				<a sveltekit:prefetch href={`${artist}/${song.trackId}`}>
					<p>{song.trackName}</p>
				</a>
			</li>
		{/each}
	</ul>
</section>
