<script lang="ts">
	import Message from './Message.svelte';
	import { FirebaseApp, Doc, Collection, User } from 'sveltefire';
	import { auth, db as firestore } from '../lib/firebase';
	import { query, collection, orderBy, limit } from 'firebase/firestore';

	import { PUBLIC_ROOM_NAME } from '$env/static/public';
	import { onMount } from 'svelte';

	const chatCollection = collection(firestore, `${PUBLIC_ROOM_NAME}/messages`);

	$: buildQuery = () => {
		return query(chatCollection, orderBy('createdAt', 'desc'), limit(50));
	};

	onMount(() => {
		setTimeout(() => {
			window.scrollTo({
				top: document.body.scrollHeight,
				behavior: 'smooth'
			});
		}, 1500);
	});
</script>

<svelte:head>
	<title>holis</title>
	<meta name="description" content="holis" />
</svelte:head>

<section>
	<FirebaseApp {auth} {firestore}>
		<User>
			<Doc ref={PUBLIC_ROOM_NAME}>
				<Collection ref={buildQuery()} let:data={messages}>
					{#each [...messages].reverse() as message}
						<Message {message} />
					{/each}
				</Collection>
			</Doc>
		</User>
	</FirebaseApp>
</section>
