<script lang="ts">
	import { isFilled, type Content } from '@prismicio/client';
	import { PrismicImage, PrismicLink } from '@prismicio/svelte';

	import Bounded from '$lib/components/Bounded.svelte';
	import PrismicRichText from '$lib/components/PrismicRichText.svelte';

	import Heading from './Heading.svelte';
	//{slice.primary.direction_right}
	export let slice: Content.HeroSlice;
</script>

{#if slice.variation === 'default'}
	<section
		class="relative bg-slate-900 text-white"
		data-slice-type={slice.slice_type}
		data-slice-variation={slice.variation}
	>
		{#if isFilled.image(slice.primary.backgroundImage)}
			<PrismicImage
				field={slice.primary.backgroundImage}
				alt=""
				class="absolute inset-0 h-full w-full pointer-events-none select-none object-cover opacity-40"
			/>
		{/if}
		<Bounded tag="div" yPadding="lg" class="relative">
			<div class="grid justify-items-center gap-8">
				<div class="max-w-2xl text-center">
					<PrismicRichText
						field={slice.primary.text}
						components={{
							heading1: Heading
						}}
					/>
				</div>
				{#if isFilled.link(slice.primary.buttonLink)}
					<PrismicLink
						field={slice.primary.buttonLink}
						class="rounded bg-white px-5 py-3 font-medium text-slate-800"
					>
						{slice.primary.buttonText || 'Learn More'}
					</PrismicLink>
				{/if}
			</div>
		</Bounded>
	</section>
{/if}
{#if slice.variation === 'heroTextLeftImageRight'}
	<section
		class="grid grid-cols-1 gap-4 items-center md:flex max-w-7xl mx-auto h-full max-h-[1200px] w-full max-md:max-w-full py-6 md:py-10 lg:py-14"
		data-slice-type={slice.slice_type}
		data-slice-variation={slice.variation}
	>
		<div class="flex flex-col px-4 mx-auto max-w-3xl min-w-[240px] w-full max-md:max-w-full">
			<!-- <PrismicRichText field={slice.primary.text} /> -->

			<div class="grid grid-cols-1 justify-items-center md:justify-items-start gap-4 md:gap-8">
				<h2
					class="overflow-hidden max-w-full text-3xl text-center md:text-left md:text-4xl lg:text-5xl font-black leading-[52px] text-sky-900 max-md:max-w-full max-md:text-4xl max-md:leading-10"
				>
					{slice.primary.heroheading}
				</h2>
				<div class="max-w-2xl text-2xl text-center md:text-left">
					<PrismicRichText
						field={slice.primary.text}
						components={{
							heading3: Heading
						}}
					/>
				</div>
				{#if isFilled.link(slice.primary.buttonLink)}
					<PrismicLink
						field={slice.primary.buttonLink}
						class="px-6 py-3.5 w-full max-w-sm my-auto bg-cyan-700 rounded  max-md:px-5 text-center text-white"
					>
						{slice.primary.buttonText || 'Learn More'}
					</PrismicLink>
				{/if}
			</div>
		</div>

		<div class={`mx-auto  ${slice.primary.direction_right ? 'md:order-first' : 'md:order-last'}`}>
			<PrismicImage
				field={slice.primary.hero_image_right}
				alt=""
				class="object-contain shrink-0 self-stretch my-auto rounded-3xl aspect-square min-w-[240px] w-[372px]"
			/>
		</div>
	</section>
{/if}
