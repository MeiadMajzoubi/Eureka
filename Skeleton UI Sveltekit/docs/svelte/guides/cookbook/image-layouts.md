# Image Layouts

Layouts for displaying sets of images.

## Grid

```svelte
<section class="grid grid-cols-2 gap-6 md:grid-cols-3">
	<!-- Row -->
	<img class="w-48 h-48 bg-surface-500 rounded-container" src="https://picsum.photos/192/192?random=1" alt="" />
	<img class="w-48 h-48 bg-surface-500 rounded-container" src="https://picsum.photos/192/192?random=2" alt="" />
	<img class="w-48 h-48 bg-surface-500 rounded-container" src="https://picsum.photos/192/192?random=3" alt="" />
	<!-- Row -->
	<img class="w-48 h-48 bg-surface-500 rounded-container" src="https://picsum.photos/192/192?random=4" alt="" />
	<img class="w-48 h-48 bg-surface-500 rounded-container" src="https://picsum.photos/192/192?random=5" alt="" />
	<img class="w-48 h-48 bg-surface-500 rounded-container" src="https://picsum.photos/192/192?random=6" alt="" />
	<!-- Row -->
	<img class="w-48 h-48 bg-surface-500 rounded-container" src="https://picsum.photos/192/192?random=7" alt="" />
	<img class="w-48 h-48 bg-surface-500 rounded-container" src="https://picsum.photos/192/192?random=8" alt="" />
	<img class="w-48 h-48 bg-surface-500 rounded-container" src="https://picsum.photos/192/192?random=9" alt="" />
</section>

```

## Quad

```svelte
<section class="grid grid-cols-2 gap-4">
	<!-- Row -->
	<img class="h-64 w-64 bg-surface-500 rounded-container" src="https://picsum.photos/256/256?random=1" alt="" />
	<img class="h-64 w-64 bg-surface-500 rounded-container" src="https://picsum.photos/256/256?random=2" alt="" />
	<!-- Row -->
	<img class="h-64 w-64 bg-surface-500 rounded-container" src="https://picsum.photos/256/256?random=3" alt="" />
	<img class="h-64 w-64 bg-surface-500 rounded-container" src="https://picsum.photos/256/256?random=4" alt="" />
</section>

```

## Masonry

```svelte
<section class="grid grid-cols-2 gap-4 md:grid-cols-4">
	<!-- Column -->
	<div class="grid gap-4">
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/320?random=1" alt="" />
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/120?random=2" alt="" />
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/280?random=3" alt="" />
	</div>
	<!-- Column -->
	<div class="grid gap-4">
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/300?random=4" alt="" />
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/280?random=5" alt="" />
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/140?random=6" alt="" />
	</div>
	<!-- Column -->
	<div class="grid gap-4">
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/280?random=7" alt="" />
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/320?random=8" alt="" />
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/140?random=9" alt="" />
	</div>
	<!-- Column -->
	<div class="grid gap-4">
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/320?random=10" alt="" />
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/140?random=11" alt="" />
		<img class="bg-surface-500 rounded-container" src="https://picsum.photos/220/280?random=12" alt="" />
	</div>
</section>

```

## Featured

```svelte
<section class="grid gap-4">
	<!-- Featured -->
	<header>
		<img class="h-auto max-w-full bg-surface-500 rounded-container" src="https://picsum.photos/960/512?random=1" alt="Featured" />
	</header>
	<!-- Row -->
	<div class="grid grid-cols-5 gap-4">
		<img class="h-full w-full bg-surface-500 rounded-container" src="https://picsum.photos/200/200?random=2" alt="" />
		<img class="h-full w-full bg-surface-500 rounded-container" src="https://picsum.photos/200/200?random=3" alt="" />
		<img class="h-full w-full bg-surface-500 rounded-container" src="https://picsum.photos/200/200?random=4" alt="" />
		<img class="h-full w-full bg-surface-500 rounded-container" src="https://picsum.photos/200/200?random=5" alt="" />
		<img class="h-full w-full bg-surface-500 rounded-container" src="https://picsum.photos/200/200?random=6" alt="" />
	</div>
</section>

```

## Attribution

Images courtesy of [Lorem Picsum](https://picsum.photos/). Markup and styles inspired by [Flowbite](https://flowbite.com/docs/components/gallery/#masonry-grid).
