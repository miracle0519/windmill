<script lang="ts">
	import { ChevronDown, ChevronUp } from 'lucide-svelte'
	import { slide } from 'svelte/transition'
	import Button from './common/button/Button.svelte'

	export let text: string
	export let view = false
</script>

<Button color="light" on:click={() => (view = !view)} variant="border"
	>{text}
	{#if !view}<ChevronDown />{:else}<ChevronUp />{/if}</Button
>
{#if view}
	<div class="my-4 px-2" transition:slide><slot /></div>
{/if}
