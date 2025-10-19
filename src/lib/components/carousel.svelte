<script lang="ts">
	import * as Card from '$lib/components/ui/card/index.js';
	import * as Carousel from '$lib/components/ui/carousel/index.js';
	import BannerImg from '../images/bannerImg.avif';
	import BannerImg1 from '../images/Bar-2.avif';
	import Autoplay from 'embla-carousel-autoplay';

	export let images: Array<any> = [];
	export let jump = true;
</script>

<Carousel.Root
	plugins={[
		Autoplay({
			delay: 4000,
			jump: jump,
			duration: 500
		})
	]}
	opts={{ loop: true, slidesToScroll: 'auto' }}
	class="w-full  h-full m-0"
>
	<Carousel.Content class="h-[60vh] lg:h-[80vh] w-full p-0">
		{#each images as image, i}
		<Carousel.Item class="h-full w-full">
			<picture>
				{#if image && image.sources && Array.isArray(image.sources)}
				{#each image.sources as source}
				<source srcset={source.srcset} type={source.type} />
				{/each}
				{/if}
				<img
				  src={image.img.src}
				  alt=""
				  fetchpriority="high"
				  decoding="async"
				  loading={i === 0 ? "eager" : "lazy"}
				  class="w-full h-full object-cover"
			 />
			</picture>
		</Carousel.Item>
		{/each}

	</Carousel.Content>
</Carousel.Root>

<style>
	.hide {
		outline: 0;
		cursor: pointer;
		background-color: transparent;
		touch-action: manipulation;
		position: absolute;
		z-index: 1;
		top: 50%;
		transform: translateY(-50%);
		border: 0;
		width: 30px;
		height: 30px;
		justify-content: center;
		align-items: center;
		fill: #1bcacd;
		padding: 0;
	}
</style>
