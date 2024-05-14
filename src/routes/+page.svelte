<script lang="ts">
	import { graphql } from 'gql.tada';
	import { getContextClient, queryStore } from '@urql/svelte';

	const client = getContextClient();

	const albumsQuery = graphql(`
		query albumsQuery {
			albums {
				id
				title
			}
		}
	`);

	$: albums = queryStore({ client, query: albumsQuery });

	$: console.log($albums);
</script>

<h1>Albums</h1>

{#if $albums.fetching}
	<p>Loading...</p>
{:else if $albums.error}
	<p>Error: {$albums.error.message}</p>
{:else if $albums.data}
	<ul>
		{#each $albums?.data.albums as album}
			<li>{album.id}</li>
			<li>{album.title}</li>
		{/each}
	</ul>
{/if}
