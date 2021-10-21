<script context="module">
	// See for Types: https://kit.svelte.dev/docs#loading
	export async function load({ page }) {
		const post = {
			title: page.params.slug,
			date: new Date(),
			body: 'lorem ipsum'
		};

		return {
			props: {
				post
			}
		};
	}
</script>

<script>
	export let post;
</script>

<h3 class="text-4xl text-center my-8">{post.title}</h3>
<p>You can add multiple params to your route e.g. [slug]-[date].svelte</p>
