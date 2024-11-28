<script>
	import { onMount } from 'svelte';
	/**
	 * @type {any[]}
	 */
	let posts = [];
	onMount(async () => {
		fetch('https://mediumpostsapi.vercel.app/api/lgarner_26737')
			.then((response) => response.json())
			.then((data) => (posts = data.dataMedium));
	});

	// let featuredPost = posts[0];
	// let otherPosts = posts.slice(1, 3);
	// console.log('featuredPost', featuredPost);
</script>

<div class="flex gap-4 justify-center">
	{#each posts as post, index}
		{#if index === 0}
			<article
				class="mb-6 p-4 bg-slate-200 shadow-sm hover:shadow-md transition-shadow rounded-2xl"
			>
				<div>
					<img src={post.image} alt={post.title} class="w-full h-48 object-cover rounded-t-2xl" />
				</div>
				<h2 class="text-xl font-semibold mb-2">
					<a
						href={post.link}
						class="text-blue-600 hover:text-blue-800 transition-colors"
						target="_blank"
						rel="noopener noreferrer"
					>
						{post.title}
					</a>
				</h2>
				<div class="mb-2 flex flex-wrap gap-2">
					{#each post.tags as tag}
						<span class="text-xs bg-gray-100 px-2 py-1 rounded">
							{tag}
						</span>
					{/each}
				</div>

				<p class="text-gray-600 mb-2">{post.description}</p>
				<div class="text-sm text-gray-500">
					<time dateTime={post.date}>
						{new Date(post.date).toLocaleDateString()}
					</time>
				</div>
			</article>
		{:else}
			<article
				class="mb-6 p-4 bg-slate-200 shadow-sm hover:shadow-md transition-shadow rounded-2xl max-w-56"
			>
				<div>
					<img src={post.image} alt={post.title} class="w-full h-48 object-cover rounded-t-2xl" />
				</div>
				<h2 class="text-xl font-semibold mb-2">
					<a
						href={post.link}
						class="text-blue-600 hover:text-blue-800 transition-colors"
						target="_blank"
						rel="noopener noreferrer"
					>
						{post.title}
					</a>
				</h2>
				<div class="mb-2 flex flex-wrap gap-2">
					{#each post.tags as tag}
						<span class="text-xs bg-gray-100 px-2 py-1 rounded">
							{tag}
						</span>
					{/each}
				</div>

				<p class="text-gray-600 mb-2">{post.description}</p>
				<div class="text-sm text-gray-500">
					<time dateTime={post.date}>
						{new Date(post.date).toLocaleDateString()}
					</time>
				</div>
			</article>
		{/if}
	{:else}
		<h2 class=" text-xl animate-pulse">Loading...</h2>
	{/each}
</div>
