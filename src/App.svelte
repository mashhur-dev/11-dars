<script lang="ts">
	import type { text } from "svelte/internal";

	let pupils: string[] = [
		"Arslon",
		"Otabek",
		"Jahongir",
		"Firdavs",
		"Sevinchbek",
		"Mashhurbek",
		"Islam",
		"Hasanboy",
		"Komron",
		"Joshqin",
	];

	type Post = {
		userId: number;
		id: number;
		title: string;
		body: string;
	};

	let posts: Post[] = [];

	let promise: Promise<Response> = fetch(
		"https://jsonplaceholder.typicode.com/posts"
	);

	promise
		.then((mashhurbek) => mashhurbek.text())
		.then((text) => {
			const array = JSON.parse(text);
			posts = array;
		});
	function remove(id: number) {
		posts = posts.filter((post) => post.id != id);
	}

	function removes() {
		posts = posts.filter((item) => typeof item.id == "string");
	}
</script>

<h1 class="ms-1">Post</h1>

<div class="d-flex gap-2 flex-wrap">

	<button on:click={() => removes()} class="btn btn-danger">Delete All</button>

	{#each posts as item}
		<div class="card m-3" style="width: 250px;">
			<div class="card-body">
				<h3>{item.id}: {item.title}</h3>
				<p>{item.body}</p>
				<button on:click={() => remove(item.id)} class="btn btn-primary">
					Delete
				</button>
			</div>
		</div>
		{/each}	
</div>
