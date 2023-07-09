<script>
	import { Navbar, NavBrand, Button } from 'flowbite-svelte';
	import { auth } from '../lib/firebase';
	import { GoogleAuthProvider, signInWithPopup } from 'firebase/auth';
	import { userStore } from 'sveltefire';
	import waving from '../lib/images/waving.svg';

	const user = userStore(auth);
	const provider = new GoogleAuthProvider();
</script>

<div>
	<Navbar navClass="px-2 sm:px-4 py-2.5 fixed w-full z-20 top-0 left-0 border-b">
		<NavBrand href="/">
			<img src={waving} class="mr-3 h-6 sm:h-9" alt="holis" />
			<span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">holis</span>
		</NavBrand>
		{#if $user}
			<p>logged in as <strong>{$user.displayName?.split(' ')[0]}</strong></p>
			<div class="flex md:order-2">
				<Button on:click={() => auth.signOut()} size="sm">logout</Button>
			</div>
		{:else}
			<div class="flex md:order-2">
				<Button on:click={() => signInWithPopup(auth, provider)} size="sm">login with google</Button
				>
			</div>
		{/if}
	</Navbar>
</div>
