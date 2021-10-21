<script context="module">
	export async function load() {
		// NOTE You don't have to access the page object.
		// Vite allows you to import all posts at once
		const posts = import.meta.globEager('../../posts/*.md');
		// console.log('posts:', posts); // { ../posts/hello.md: Module {default, metadata}}
		// console.log('posts', Object.values(posts)); // Module[] */
		const postsList = Object.values(posts); // Module[]
		const postsMeta = postsList.map((post) => {
			return post.metadata;
		});
		console.log('postsMeta:', postsMeta); // Post[]

		// NOTE You still need to return something from load() eg return {}
		return {
			props: {
				posts: postsMeta
			}
		};
	}
</script>

<script>
	export let posts;
</script>

<!-- NOTE __layout.reset.svelte layouts allow you to ignore the root layout -->
<div>
	<slot />
	<aside>
		<h5>Archive</h5>
		<ul>
			{#each posts as post}
				<li><a href={`/posts/${post.slug}`}>{post.title}</a></li>
			{/each}
		</ul>
	</aside>
</div>
