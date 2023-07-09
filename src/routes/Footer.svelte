<script lang="ts">
	import { Button, Footer, Input, DarkMode } from 'flowbite-svelte';
	import { User } from 'sveltefire';
	import { db as firestore } from '../lib/firebase';
	import { addDoc, collection } from 'firebase/firestore';
	import { PUBLIC_ROOM_NAME } from '$env/static/public';

	const chatCollection = collection(firestore, `${PUBLIC_ROOM_NAME}/messages`);

	let msg = '';
</script>

<div>
	<Footer class="fixed bottom-0 left-0 z-20 w-full" style="display: block">
		<User let:user>
			<form
				on:submit|preventDefault={async () => {
					const newMessage = {
						text: msg,
						createdAt: Date.now(),
						name: user.displayName,
						userId: user.uid,
						photoUrl: user.photoURL
					};
					msg = '';
					await addDoc(chatCollection, newMessage);
					requestAnimationFrame(() =>
						window.scrollTo({
							top: document.body.scrollHeight,
							behavior: 'smooth'
						})
					);
				}}
			>
				<div class="flex ml-auto mr-auto" style="max-width: 57.625rem">
					<Input placeholder="message" bind:value={msg} required class="mr-3" />
					<Button type="submit" class="mr-2">send</Button>
					<DarkMode />
				</div>
			</form>
		</User>
	</Footer>
</div>
