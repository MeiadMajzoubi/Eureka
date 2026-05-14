# Breadcrumbs

Displays the current navigation hierarchy.

```svelte
<ol class="flex items-center gap-4">
	<li><a class="opacity-60 hover:underline" href="#">Blog</a></li>
	<li class="opacity-50" aria-hidden>&rsaquo;</li>
	<li><a class="opacity-60 hover:underline" href="#">Category</a></li>
	<li class="opacity-50" aria-hidden>&rsaquo;</li>
	<li>Article</li>
</ol>

```

## Icons

Feel free to mix in icons for the anchor labels or separators.

```svelte
<script lang="ts">
	import { ChevronRightIcon, CogIcon, HouseIcon } from '@lucide/svelte';
</script>

<ol class="flex items-center gap-4">
	<li>
		<a class="opacity-60 hover:opacity-100" href="#">
			<HouseIcon size={24} />
		</a>
	</li>
	<li class="opacity-50" aria-hidden>
		<ChevronRightIcon size={14} />
	</li>
	<li>
		<a class="opacity-60 hover:opacity-100" href="#">
			<CogIcon size={24} />
		</a>
	</li>
	<li class="opacity-50" aria-hidden>
		<ChevronRightIcon size={14} />
	</li>
	<li>Current</li>
</ol>

```
