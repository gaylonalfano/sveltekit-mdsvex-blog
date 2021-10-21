<script context="module">
	// See for Types: https://kit.svelte.dev/docs#loading
	export async function load({ page }) {
		// Dynamic import
		// NOTE Use .default to grab the ProxyComponent. Remove it and you have Module {}
		// that holds both default AND metadata objects (where Frontmatter is stored)
		const Hello = await import(`../../posts/${page.params.slug}.md`);
		console.log('Hello:', Hello); // Module {default, metadata}

		// const post = {
		// 	title: page.params.slug,
		// 	date: new Date(),
		// 	body: 'lorem ipsum'
		// };

		return {
			props: {
				Hello: Hello.default,
				title: Hello.metadata.title, // From MD Frontmatter!
				date: Hello.metadata.date
			}
		};
	}
</script>

<script>
	/* import Hello from '../../posts/hello.md'; */

	export let Hello;
	export let title; // You can extract other data from MD files Frontmatter
	export let date;
	/* export let post; */
</script>

<h2>{title}</h2>
<p>I can pull in the 'date' metadata as well: {date}</p>

<Hello />
