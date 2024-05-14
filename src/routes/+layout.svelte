<script>
	import { Client, cacheExchange, setContextClient, fetchExchange } from '@urql/svelte';

	const client = new Client({
		url: 'https://probable-pheasant-69.hasura.app/v1/graphql',
		exchanges: [cacheExchange, fetchExchange],
		fetchOptions: () => {
			// const token = getToken();
			const hasuraAdminSecret = import.meta.env.VITE_HASURA_ADMIN_SECRET;
			return {
				// headers: { authorization: token ? `Bearer ${token}` : '' }
				headers: {
					'x-hasura-admin-secret': hasuraAdminSecret
				}
			};
		}
	});

	setContextClient(client);
</script>

<main>
	<slot></slot>
</main>
