<script lang="ts">
	import { createEventDispatcher, getContext } from 'svelte'
	import type { AppEditorContext, GridItem } from '../types'

	import ComponentPanel from './settingsPanel/ComponentPanel.svelte'
	import TablePanel from './TablePanel.svelte'

	const { selectedComponent } = getContext<AppEditorContext>('AppEditorContext')

	export let gridItems: GridItem[]
</script>

{#each gridItems as gridItem (gridItem.data.id)}
	{#if gridItem.data.id === $selectedComponent}
		<ComponentPanel bind:gridItems bind:component={gridItem.data} />
	{:else if gridItem.data.type === 'tablecomponent'}
		<TablePanel bind:component={gridItem.data} />
	{:else if gridItem.data.subGrids}
		{#each gridItem.data.subGrids as subGrid}
			<svelte:self bind:gridItems={subGrid} />
		{/each}
	{/if}
{/each}
