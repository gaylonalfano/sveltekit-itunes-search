<script context="module">
	export async function load({ page, fetch, session, stuff }) {
		// load() runs before rendering the content of the page
		// Want to make a fetch() to the API using page.params
		const response = await fetch(
			`https://itunes.apple.com/search?term=${page.params.trackId}&entity=song`
		);
		const data = await response.json();

		const song = data.results[0];
		console.log(song);

		// Now return Object with props property and add our pokeman data
		// NOTE Again, this all runs BEFORE Svelte renders anything!
		return { props: { song } };
	}
</script>

<script>
	export let song;
</script>

<section>
	<div>{song.trackName}</div>
</section>
