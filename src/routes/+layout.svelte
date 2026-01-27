<script>
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();

	import "$lib/styles.css";
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<link rel="stylesheet" href="https://css.hackclub.com/theme.css">
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Gabarito:wght@400..900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Playwrite+DK+Loopet:wght@100..400&display=swap" rel="stylesheet">
</svelte:head>

{@render children()}
