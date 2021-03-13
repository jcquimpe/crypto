<script>
	import Tailwindcss from './Tailwindcss.svelte';
	import Router from 'svelte-spa-router';
	import SignIn from './routes/SignIn.svelte';
	import SignUp from './routes/SignUp.svelte';
	import ForgotPassword from './routes/ForgotPassword.svelte';
	import {userbaseStore, userStore, promiseStore} from "./stores";
	const userbase = window.userbase;
	window.userbase = null;

	//stores
	$userbaseStore = userbase;
	$userStore = null;

	$promiseStore = userbase.init({appId: '5e818c6b-c188-49b4-8ab5-0ae7c08c7cf0'})
		.then((session) => $userStore = session.user);

	function signout(){
		$promiseStore = $userbaseStore.signOut().then(() => $userStore = null)
	}
</script>

<Tailwindcss />

<div class =  "text-gray-400 bg-gray-500 body-font" style="
	background-image: url('../../bg2.jpg');
	background-repeat: no-repat;
	background-size: cover;
	background-blend-mode: multiply;">
	<div class="container flex flex-col justify-center items-center w-screen h-screen mx-auto">
		{#await $promiseStore}
			Loading..
		{:then _}
			{#if $userStore}
					<h1 class = "font-large text-4xl text-white font-anton">Welcome, {$userStore.username}!</h1> 
					<h3>You have successfully registered</h3>
					<button on:click={signout}>Logout</button>
			{:else}
				<Router routes = {{
					'/': SignIn,
					'/SignUp': SignUp,
					'/ForgotPassword': ForgotPassword
				}} />
			{/if}
			{:catch error}
				<strong>Error!{error}</strong>
		{/await}
	</div>
</div>