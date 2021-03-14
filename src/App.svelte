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
	
		{#await $promiseStore}
			Loading...
		{:then _}
			{#if $userStore}

			<div class="flex-center position-ref full-height">
				<div class="top-right mr-auto">
					<span class = "font-large text-white font-anton">Welcome, {$userStore.username}!</span> 
					<button on:click={signout} class="text-white bg-purple-700 border-0 py-1 px-2 items-center focus:outline-none hover:bg-purple-500 rounded">Logout</button>
				</div>
				<div class="content">
					<h3>You have successfully registered</h3>
				</div>
			</div>
	


					
					
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