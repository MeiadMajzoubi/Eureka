# Dialog Element

Implement a simple popup dialog using the native HTML element.

```svelte
<script lang="ts">
	let dialogRef: HTMLDialogElement;

	function showModal() {
		dialogRef?.showModal();
	}

	function closeModal() {
		dialogRef?.close();
	}
</script>

<!-- Dialog -->
<dialog
	bind:this={dialogRef}
	class="rounded-container bg-surface-100-900 text-inherit max-w-[640px] top-1/2 left-1/2 -translate-1/2 p-4 space-y-4 z-10 backdrop:bg-surface-50/75 dark:backdrop:bg-surface-950/75"
>
	<h2 class="h3">Hello world!</h2>
	<p>This is an example popover created using the native Dialog element.</p>
	<form method="dialog" class="flex justify-end">
		<button type="button" class="btn preset-tonal" onclick={closeModal}>Close</button>
	</form>
</dialog>
<!-- Interface -->
<div class="flex justify-center items-center">
	<!-- Trigger -->
	<button class="btn preset-filled" onclick={showModal}>Open Modal</button>
</div>

<style>
	/* NOTE: add the following styles to your global stylesheet. */
	dialog,
	dialog::backdrop {
		--anim-duration: 250ms;
		transition:
			display var(--anim-duration) allow-discrete,
			overlay var(--anim-duration) allow-discrete,
			opacity var(--anim-duration);
		opacity: 0;
	}
	/* Animate In */
	dialog[open],
	dialog[open]::backdrop {
		opacity: 1;
	}
	/* Animate Out */
	@starting-style {
		dialog[open],
		dialog[open]::backdrop {
			opacity: 0;
		}
	}
</style>

```

## How It Works

This is enabled by the native [Dialog](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog) element, which includes a dedicated Javascript API for toggling the display.

## Animations

Animating `display: none` with CSS alone has limited browser support. However, per the video below, we can use progressive enhancement our dialog to ensure animations degrade gracefully for unsupported browsers.

<iframe class="w-full aspect-video" src="https://www.youtube.com/embed/vmDEHAzj2XE?si=GTYFY9dk013lL0Y3" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen />

## Alternatives

If you need finer grain control, consider Skeleton's integration guides for [Floating UI](https://floating-ui.com/).

* [Skeleton Popovers](/docs/\[framework]/framework-components/popover) - powered by Zag.js.
