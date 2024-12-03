<script lang="ts">
	import Heading from '$lib/components/Heading.svelte';
	import PrismicRichText from '$lib/components/PrismicRichText.svelte';

	export let card;
	// console.log('card', card);
</script>

<li class="grid gap-8 max-w-80">
	<div class="leading-relaxed border border-gray-900 rounded-lg p-6 bg-white">
		<div class="text-2xl font-semibold mb-5 text-center">
			<PrismicRichText field={card.text} />
			<!-- <Heading
				as="h2"
				size="3xl"
				id={card.text
					.toLowerCase()
					.replace(/[^\w\s-]/g, '')
					.replace(/[\s_-]+/g, '-')
					.replace(/(^-|-$)/g, '')}
			>
				{card.text}
			</Heading> -->
		</div>
		<div>
			<PrismicRichText field={card.card_content} />
		</div>
	</div>
</li>
