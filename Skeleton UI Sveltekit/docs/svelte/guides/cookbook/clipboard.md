# Clipboard API

Learn how to integrate the native browser clipboard API.

## How It Works

Refer to the [Clipboard API](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API) documentation for details.

## Programmatic

```svelte
<script lang="ts">
	async function handleCopy() {
		const data = 'Hello World!';
		await navigator.clipboard.writeText(data);
		alert(`Copied "${data}" to clipboard!`);
	}
</script>

<button class="btn preset-filled" onclick={handleCopy}>Copy to Clipboard</button>

```

## Using Inputs

```svelte
<script lang="ts">
	let value = $state('Hello Skeleton');

	async function handleCopy() {
		await navigator.clipboard.writeText(value);
		alert(`Copied "${value}" to clipboard!`);
	}
</script>

<div class="flex items-center gap-4">
	<input type="text" class="input" bind:value />
	<button class="btn preset-filled" onclick={handleCopy}>Copy</button>
</div>

```
