<script>
	import Album from './Album.svelte'
	let title = 'My Dog Album'
</script>

<main>
	<Album {title} />
</main>

<style>
	main {
		text-align: center;
		padding: 1em; /* em = ukuran font default = 16px */
		margin: 0 auto;
		background: rgb(240, 240, 240);
		height: 100vh; /* vh = viewport height */
	}
</style>