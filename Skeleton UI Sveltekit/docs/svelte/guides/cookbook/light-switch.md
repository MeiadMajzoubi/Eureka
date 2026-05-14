# Light Switch

Learn how to create a Light Switch toggle.

Use [Dark Mode](/docs/\[framework]/guides/mode) to make use of either a base or `dark:` variant for your utility class styles. By default, Tailwind uses the `prefers-color-scheme` media query to determine and match the user's operating system settings. However, if you wish to provide your users manual control, you'll need to adjust the Dark Mode strategy for Tailwind, as well as provide the toggle interface (aka a light switch). This guide will show you how to fulfill both requirements.

<Process>
  <ProcessStep step="1">
    ## Adjust the Dark Mode Strategy

    Open your global stylesheet and set the following variant:

    ```css
    @custom-variant dark (&:where([data-mode="dark"], [data-mode="dark"] *));
    ```

    Then set the following data attribute on your application's `<html>` element for light mode:

    ```html
    <html data-mode="light"></html>
    ```

    Or for dark mode:

    ```html
    <html data-mode="dark"></html>
    ```
  </ProcessStep>

  <ProcessStep step="2">
    ## Create the Component

    We'll create a implementation of the Switch component that can toggle the mode on demand.

    ```svelte
    <script lang="ts">
    	import { Switch } from '@skeletonlabs/skeleton-svelte';

    	let checked = $state(false);

    	$effect(() => {
    		const mode = localStorage.getItem('mode') || 'light';
    		checked = mode === 'dark';
    	});

    	const onCheckedChange = (event: { checked: boolean }) => {
    		const mode = event.checked ? 'dark' : 'light';
    		document.documentElement.setAttribute('data-mode', mode);
    		localStorage.setItem('mode', mode);
    		checked = event.checked;
    	};
    </script>

    <svelte:head>
    	<script>
    		document.documentElement.setAttribute('data-mode', localStorage.getItem('mode') || 'dark');
    	</script>
    </svelte:head>

    <Switch {checked} {onCheckedChange}>
    	<Switch.Control>
    		<Switch.Thumb />
    	</Switch.Control>
    	<Switch.HiddenInput />
    </Switch>
    ```
  </ProcessStep>

  <ProcessStep step="3">
    ## Import the Component

    We'll then add the component to our app. Make sure to set the correct path.

    ```svelte
    <script lang="ts">
    	import Lightswitch from './path/to/Lightswitch.svelte';
    </script>

    <Lightswitch />
    ```
  </ProcessStep>
</Process>

## User Interface

While we utilize a primitive Switch for the minimal example above, feel free to adjust the logic and interface to your preference. We provide a more detailed [Switch example](/docs/\[framework]/framework-components/switch#icons).
