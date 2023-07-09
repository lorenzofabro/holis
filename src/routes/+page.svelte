<script lang="ts">
	import { FirebaseApp, Doc, Collection, User } from 'sveltefire';
	import { auth, db as firestore } from '../lib/firebase';
	import { query, collection, orderBy } from 'firebase/firestore';
	import Message from './Message.svelte';

	const documentName = 'chats/room_1';
	const chatCollection = collection(firestore, `${documentName}/messages`);

	$: buildQuery = () => {
		return query(chatCollection, orderBy('createdAt', 'desc'));
	};
</script>

<svelte:head>
	<title>holis</title>
	<meta name="description" content="holis" />
</svelte:head>

<section>
	<FirebaseApp {auth} {firestore}>
		<User>
			<Doc ref={documentName}>
				<Collection ref={buildQuery()} let:data={messages}>
					{#each messages as message}
						<Message {message} />
					{/each}
				</Collection>
			</Doc>
		</User>
	</FirebaseApp>
</section>
