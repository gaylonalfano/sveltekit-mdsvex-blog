<script context="module">
	// See for Types: https://kit.svelte.dev/docs#loading
	export async function load({ page }) {
		try {
			// Dynamic import
			// NOTE Use .default to grab the ProxyComponent. Remove it and you have Module {}
			// that holds both default AND metadata objects (where Frontmatter is stored)
			const Post = await import(`../../posts/${page.params.slug}.md`);
			console.log('Post:', Post); // Module {default, metadata}

			// const post = {
			// 	title: page.params.slug,
			// 	date: new Date(),
			// 	body: 'lorem ipsum'
			// };

			return {
				props: {
					Post: Post.default,
					title: Post.metadata.title, // From MD Frontmatter!
					date: Post.metadata.date
				}
			};
		} catch (e) {
			console.log(e);
			// NOTE Can redirect to a valid URL using redirect and status 303
			// return {
			// 	status: 303,
			// 	redirect: '/posts'
			// };
			// NOTE Or we can return a 404
			return {
				status: 404,
				error: 'Post not found'
			};
		}
	}
</script>

<script>
	// NOTE Can import here or inside the load() function
	/* import Hello from '../../posts/hello.md'; */

	export let Post;
	// export let title; // You can extract other data from MD files Frontmatter
	// export let date;
	/* export let post; */
</script>

<!-- <Post /> is not reactive. Need the svelte:component below instead -->
<svelte:component this={Post} />
