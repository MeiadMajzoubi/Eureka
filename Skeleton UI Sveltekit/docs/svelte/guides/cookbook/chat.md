# Chat

Create a custom chat feed or AI prompt interface.

```svelte
<script lang="ts">
	import { SendIcon } from '@lucide/svelte';
	import { onMount } from 'svelte';

	// Types
	interface Person {
		id: number;
		avatar: number;
		name: string;
	}
	interface MessageFeed {
		id: number;
		host: boolean;
		avatar: number;
		name: string;
		timestamp: string;
		message: string;
		color: string;
	}

	let elemChat: HTMLElement;
	const lorem =
		'Lorem, ipsum dolor sit amet consectetur adipisicing elit. Provident blanditiis quidem dolorum ab similique. Voluptatibus quibusdam unde mollitia corrupti assumenda libero. Quibusdam culpa illum unde asperiores accusantium! Unde, cupiditate tenetur.';

	// Navigation List
	const people: Person[] = [
		{ id: 0, avatar: 14, name: 'Michael' },
		{ id: 1, avatar: 40, name: 'Janet' },
		{ id: 2, avatar: 31, name: 'Susan' },
		{ id: 3, avatar: 56, name: 'Joey' },
		{ id: 4, avatar: 24, name: 'Lara' },
		{ id: 5, avatar: 9, name: 'Melissa' },
	];
	let currentPersonId: number = people[0].id;

	// Messages
	let messageFeed: MessageFeed[] = [
		{
			id: 0,
			host: true,
			avatar: 48,
			name: 'Jane',
			timestamp: 'Yesterday @ 2:30pm',
			message: lorem,
			color: 'preset-tonal-primary',
		},
		{
			id: 1,
			host: false,
			avatar: 14,
			name: 'Michael',
			timestamp: 'Yesterday @ 2:45pm',
			message: lorem,
			color: 'preset-tonal-primary',
		},
		{
			id: 2,
			host: true,
			avatar: 48,
			name: 'Jane',
			timestamp: 'Yesterday @ 2:50pm',
			message: lorem,
			color: 'preset-tonal-primary',
		},
		{
			id: 3,
			host: false,
			avatar: 14,
			name: 'Michael',
			timestamp: 'Yesterday @ 2:52pm',
			message: lorem,
			color: 'preset-tonal-primary',
		},
	];
	let currentMessage = '';

	function scrollChatBottom(behavior?: 'auto' | 'instant' | 'smooth') {
		elemChat.scrollTo({ top: elemChat.scrollHeight, behavior });
	}

	function getCurrentTimestamp(): string {
		return new Date().toLocaleString('en-US', { hour: 'numeric', minute: 'numeric', hour12: true });
	}

	function addMessage() {
		const newMessage = {
			id: messageFeed.length,
			host: true,
			avatar: 48,
			name: 'Jane',
			timestamp: `Today @ ${getCurrentTimestamp()}`,
			message: currentMessage,
			color: 'preset-tonal-primary',
		};
		// Update the message feed
		messageFeed = [...messageFeed, newMessage];
		// Clear prompt
		currentMessage = '';
		// Smooth scroll to bottom
		// Timeout prevents race condition
		setTimeout(() => scrollChatBottom('smooth'), 0);
	}

	function onPromptKeydown(event: KeyboardEvent) {
		if (['Enter'].includes(event.code)) {
			event.preventDefault();
			addMessage();
		}
	}

	// When DOM is mounted, scroll to bottom
	onMount(() => {
		scrollChatBottom();
	});
</script>

<section class="card bg-surface-100-900 rounded-container overflow-hidden">
	<div class="chat w-full h-full grid grid-cols-1 lg:grid-cols-[30%_1fr]">
		<!-- Navigation -->
		<div class="hidden lg:grid grid-rows-[auto_1fr_auto] border-r-[1px] border-surface-200-800">
			<!-- Header -->
			<header class="border-b-[1px] border-surface-200-800 p-4">
				<input class="input" type="search" placeholder="Search..." />
			</header>
			<!-- List -->
			<div class="p-4 space-y-4 overflow-y-auto">
				<small class="opacity-50">Contacts</small>
				<div class="flex flex-col space-y-1">
					{#each people as person (person.id)}
						<button
							type="button"
							class="card p-2 w-full flex items-center space-x-4 {person.id === currentPersonId
								? 'preset-filled-primary-500'
								: 'bg-surface-hover-token'}"
							onclick={() => (currentPersonId = person.id)}
						>
							<!-- <Avatar src="https://i.pravatar.cc/?img={person.avatar}" name={person.name} size="size-8" /> -->
							<span class="flex-1 text-start">
								{person.name}
							</span>
						</button>
					{/each}
				</div>
			</div>
			<!-- Footer -->
			<!-- <footer class="border-t-[1px] border-surface-200-800 p-4">(footer)</footer> -->
		</div>
		<!-- Chat -->
		<div class="grid grid-rows-[1fr_auto]">
			<!-- Conversation -->
			<section bind:this={elemChat} class="max-h-[500px] p-4 overflow-y-auto space-y-4">
				{#each messageFeed as bubble (bubble.id)}
					{#if bubble.host === true}
						<div class="grid grid-cols-[auto_1fr] gap-2">
							<!-- <Avatar src="https://i.pravatar.cc/?img={bubble.avatar}" name={bubble.name} size="size-12" /> -->
							<div class="card p-4 preset-tonal rounded-tl-none space-y-2">
								<header class="flex justify-between items-center">
									<p class="font-bold">{bubble.name}</p>
									<small class="opacity-50">{bubble.timestamp}</small>
								</header>
								<p>{bubble.message}</p>
							</div>
						</div>
					{:else}
						<div class="grid grid-cols-[1fr_auto] gap-2">
							<div class="card p-4 rounded-tr-none space-y-2 {bubble.color}">
								<header class="flex justify-between items-center">
									<p class="font-bold">{bubble.name}</p>
									<small class="opacity-50">{bubble.timestamp}</small>
								</header>
								<p>{bubble.message}</p>
							</div>
							<!-- <Avatar src="https://i.pravatar.cc/?img={bubble.avatar}" name={bubble.name} size="size-12" /> -->
						</div>
					{/if}
				{/each}
			</section>
			<!-- Prompt -->
			<section class="border-t-[1px] border-surface-200-800 p-4">
				<div class="input-group grid-cols-[auto_1fr_auto] divide-x divide-surface-200-800 rounded-container-token">
					<button class="input-group-cell preset-tonal">+</button>
					<textarea
						value={currentMessage}
						oninput={(e) => (currentMessage = e.currentTarget.value)}
						class="bg-transparent border-0 ring-0"
						name="prompt"
						id="prompt"
						placeholder="Write a message..."
						rows="1"
						onkeydown={onPromptKeydown}
					></textarea>
					<button class="input-group-cell {currentMessage ? 'preset-filled-primary-500' : 'preset-tonal'}" onclick={addMessage}>
						<SendIcon />
					</button>
				</div>
			</section>
		</div>
	</div>
</section>

```

## Layout Columns

Use Tailwind's [grid column](https://tailwindcss.com/docs/grid-template-columns) utility classes to define horizontal columns for your layout.

```svelte
<!--
https://tailwindcss.com/docs/grid-template-columns#arbitrary-values
- auto: size to content widths
- 1fr: fill available space evenly
- {amount}: set fixed size (ex: 320px)
-->
<div class="w-full grid grid-cols-[auto_1fr_auto] gap-1">
	<div class="bg-surface-100-900 p-4">(nav)</div>
	<div class="bg-surface-100-900 p-4">(feed)</div>
	<div class="bg-surface-100-900 p-4">(online)</div>
</div>

```

## Layout Rows

Use Tailwind's [grid row](https://tailwindcss.com/docs/grid-template-rows) utility classes to define vertical layout rows for your layout.

```svelte
<!--
https://tailwindcss.com/docs/grid-template-rows#arbitrary-values
- auto: size to content widths
- 1fr: fill available space evenly
- {amount}: set fixed size (ex: 320px)
-->
<div class="w-full grid grid-cols-2 gap-10">
	<!-- Three Row Layout -->
	<div class="h-full grid grid-rows-[auto_1fr_auto] gap-1">
		<div class="bg-surface-100-900 p-4">(search)</div>
		<div class="bg-surface-100-900 p-4">(list)</div>
		<div class="bg-surface-100-900 p-4">(footer)</div>
	</div>
	<!-- Two Row Layout -->
	<div class="h-full grid grid-rows-[1fr_auto] gap-1">
		<!-- We've set a max height here to trigger the vertical overflow. -->
		<!-- Removed max-h and space-y in your project. -->
		<div class="bg-surface-100-900 p-4 overflow-y-auto max-h-[128px] space-y-4">
			<p>(feed)</p>
			<p>
				Lorem, ipsum dolor sit amet consectetur adipisicing elit. Reprehenderit dolor ullam, qui et itaque quam distinctio dicta nostrum
				veritatis harum iure hic sequi aperiam, explicabo earum totam deserunt. Fugiat, temporibus.
			</p>
		</div>
		<div class="bg-surface-100-900 p-4">(prompt)</div>
	</div>
</div>

```

## Message Feed

The feed simply loops through the available feed data. Each `<pre>` tag represents a single *bubble* element.

```svelte
<script lang="ts">
	const messageFeed = [
		{
			id: 0,
			host: true,
			avatar: 48,
			name: 'Jane',
			timestamp: 'Yesterday @ 2:30pm',
			message: 'Some message text.',
			color: 'variant-soft-primary',
		},
		{
			id: 1,
			host: false,
			avatar: 14,
			name: 'Michael',
			timestamp: 'Yesterday @ 2:45pm',
			message: 'Some message text.',
			color: 'variant-soft-primary',
		},
	];
</script>

<section class="w-full max-h-[400px] overflow-y-auto space-y-4">
	<!-- Loop through the messageFeed array -->
	{#each messageFeed as bubble}
		{@const role = bubble.host === true ? 'host' : 'guest'}
		<!-- Render the bubble template -->
		<pre class="pre">{JSON.stringify({ role, ...bubble }, null, 2)}</pre>
	{/each}
</section>

```

## Message Bubbles

Provide styling to each bubble element.

```svelte
<script lang="ts">
	const messageFeed = [
		{
			id: 0,
			host: true,
			avatar: 48,
			name: 'Jane',
			timestamp: 'Yesterday @ 2:30pm',
			message: 'Some message text.',
			color: 'preset-tonal-primary',
		},
		{
			id: 1,
			host: false,
			avatar: 14,
			name: 'Michael',
			timestamp: 'Yesterday @ 2:45pm',
			message: 'Some message text.',
			color: 'preset-tonal-primary',
		},
	];
</script>

<section class="w-full max-h-[400px] overflow-y-auto space-y-4">
	<!-- Loop through the messageFeed array -->
	{#each messageFeed as bubble}
		{#if bubble.host}
			<!-- Host Bubble -->
			<div class="grid grid-cols-[auto_1fr] gap-2">
				<!-- <Avatar src={`https://i.pravatar.cc/?img=${bubble.avatar}`} name={bubble.name} size="size-12" /> -->
				<div class="card p-4 preset-tonal rounded-tl-none space-y-2">
					<header class="flex justify-between items-center">
						<p class="font-bold">{bubble.name}</p>
						<small class="opacity-50">{bubble.timestamp}</small>
					</header>
					<p>{bubble.message}</p>
				</div>
			</div>
		{:else}
			<!-- Guest Bubble -->
			<div class="grid grid-cols-[1fr_auto] gap-2">
				<div class={`card p-4 rounded-tr-none space-y-2 ${bubble.color}`}>
					<header class="flex justify-between items-center">
						<p class="font-bold">{bubble.name}</p>
						<small class="opacity-50">{bubble.timestamp}</small>
					</header>
					<p>{bubble.message}</p>
				</div>
				<!-- <Avatar src={`https://i.pravatar.cc/?img=${bubble.avatar}`} name={bubble.name} size="size-12" /> -->
			</div>
		{/if}
	{/each}
</section>

```

## Prompt

Use Skeleton's [input group](/docs/\[framework]/tailwind-components/forms#groups) styles to create a custom text prompt.

***

## Scroll to Bottom

Bind your scrollable feed panel element reference ([Svelte](https://svelte.dev/docs/svelte/bind) | [React](https://react.dev/learn/referencing-values-with-refs#refs-and-the-dom)), then use [scrollTo](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollTo) to scroll the panel to the bottom on demand. Scroll behavior can be set via `behavior: 'smooth'`.

```ts
function scrollChatBottom(behavior?: 'auto' | 'instant' | 'smooth' = 'smooth') {
	// `elemChat` represents our scrollable panel element
	elemChat.scrollTo({ top: elemChat.scrollHeight, behavior });
}
```

## Add a Message

Below we'll cover how to append the message feed with a new message from the host user. Per our above examples, we'll use the same `messageFeed` data structure.

```ts
let messageFeed = [
	/* ...*/
];
```

Then bind to the textarea for your prompt in order to capture any message typed by the user.

Here's an example of how we might append a new message to the `messageFeed` array.

```ts
function addMessage(): void {
	const newMessage = {
		id: messageFeed.length,
		host: true,
		avatar: 48,
		name: 'Jane',
		timestamp: new date(),
		message: elemPrompt.value,
		color: 'preset-tonal-primary',
	};
	// Append the new message to the message feed
	messageFeed = [...messageFeed, newMessage];
	// Clear the textarea message
	elemPrompt.value = '';
	// Smoothly scroll to the bottom of the feed
	setTimeout(() => {
		scrollChatBottom('smooth');
	}, 0);
}
```

This can be triggered when the prompt's SEND button is clicked.

```svelte
<button ... onclick={addMessage}>Send</button>
```
