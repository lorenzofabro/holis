<script lang="ts">
	import { Avatar, Card, P, Heading } from 'flowbite-svelte';
	import { User } from 'sveltefire';

	export let message: any;
</script>

<div>
	<User let:user>
		{#if message.userId === user.uid}
			<Card
				class="mt-2 max-w-full ml-32 items-end hover:bg-gray-100 dark:hover:bg-gray-700"
				shadow={false}
				border={false}
			>
				<div class="flex-container">
					<div class="message-container">
						<P size="base" style="text-align: end"><strong>{message.name}</strong></P>
						<P size="sm" style="text-align: end">{message.text}</P>
					</div>
					<div class="avatar" style="margin-left: 10px;">
						<Avatar src={message.photoUrl ?? ''} />
					</div>
				</div>
			</Card>
		{:else}
			<Card
				class="mt-2 max-w-full mr-32 hover:bg-gray-100 dark:hover:bg-gray-700"
				shadow={false}
				border={false}
			>
				<div class="flex-container">
					<div class="avatar" style="margin-right: 10px;">
						<Avatar src={message.photoUrl ?? ''} />
					</div>
					<div class="message-container">
						<P size="base"><strong>{message.name}</strong></P>
						<P size="sm">{message.text}</P>
					</div>
				</div>
			</Card>
		{/if}
	</User>
</div>

<style>
	.flex-container {
		display: flex;
		align-items: center;
	}

	.avatar {
		flex-shrink: 0;
	}

	.message-container {
		display: flex;
		flex-direction: column;
	}
</style>
