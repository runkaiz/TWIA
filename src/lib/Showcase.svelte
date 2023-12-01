<script>
	import Link from '$lib/Link.svelte';

	export let title = '';
	export let reference = '';
</script>

<div class="p-6 border rounded shadow space-y-4">
	<h2 class="text-2xl font-bold">{title}</h2>
	<slot />
	{#if reference != ''}
		<div>
			<Link to={reference}>Reference</Link>
		</div>
	{/if}
</div>
