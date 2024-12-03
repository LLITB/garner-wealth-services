<script lang="ts">
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	import { isFilled, type Content } from '@prismicio/client';
	import { PrismicImage, PrismicLink } from '@prismicio/svelte';

	import Bounded from '$lib/components/Bounded.svelte';
	import PrismicRichText from '$lib/components/PrismicRichText.svelte';

	import Heading from './Heading.svelte';

	//{slice.primary.direction_right}
	export let slice: Content.HeroSlice;

	onMount(() => {
		const tl = gsap.timeline({
			defaults: {
				ease: 'power2.inOut'
			}
		});

		tl.fromTo(
			'.hero__heading',
			{ scale: 0.5, opacity: 0 },
			{ scale: 1, opacity: 1, duration: 1.4 }
		);
		tl.fromTo('.hero__body', { y: 20, opacity: 0 }, { y: 0, opacity: 1, duration: 1.2 }, '-=0.5');
		tl.fromTo(
			'.hero__button',
			{ y: 20, opacity: 0, scale: 1.5 },
			{ y: 0, opacity: 1, scale: 1, duration: 1.3 },
			'-=0.8'
		);
	});
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
		class="grid grid-cols-1 gap-4 items-center md:flex max-w-7xl mx-auto h-full py-5 md:py-0 md:h-screen w-full max-md:max-w-full"
		data-slice-type={slice.slice_type}
		data-slice-variation={slice.variation}
	>
		<div class="flex flex-col px-4 mx-auto max-w-3xl min-w-[240px] w-full max-md:max-w-full">
			<!-- <PrismicRichText field={slice.primary.text} /> -->

			<div class="grid grid-cols-1 justify-items-center md:justify-items-start gap-4 md:gap-8">
				<h1
					class="hero__heading overflow-hidden max-w-full text-3xl text-center md:text-left md:text-4xl lg:text-5xl font-black leading-[52px] text-sky-900 max-md:max-w-full max-md:text-4xl max-md:leading-10"
				>
					{slice.primary.heroheading}
				</h1>
				<div class="hero__body max-w-2xl text-2xl text-center md:text-left">
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
						target="_blank"
						class="hero__button px-6 py-3.5 w-full max-w-sm my-auto bg-cyan-700 rounded  max-md:px-5 text-center text-white"
					>
						{slice.primary.buttonText || 'Learn More'}
					</PrismicLink>
				{/if}
			</div>
		</div>

		<div
			class={`mx-auto hero__body glass-container  ${slice.primary.direction_right ? 'md:order-first' : 'md:order-last'}`}
		>
			<div
				class="hero__glow hero__glow--one absolute -left-1/3 -top-5 -z-10 h-2/3 w-2/3 bg-cyan-700/40 mix-blend-screen blur-3xl filter md:blur-[120px]"
			/>
			<div
				class="hero__glow hero__glow--two absolute left-5 top-1/3 -z-10 h-2/3 w-2/3 bg-orange-600/40 mix-blend-screen blur-3xl filter md:blur-[120px]"
			/>
			<PrismicImage
				field={slice.primary.hero_image_right}
				alt=""
				class="object-contain shrink-0 self-stretch my-auto rounded-3xl aspect-square min-w-[240px] w-[372px]"
			/>
		</div>
	</section>
{/if}
