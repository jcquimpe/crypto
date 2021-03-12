<script>
	import Tailwindcss from './Tailwindcss.svelte';
	import Router from 'svelte-spa-router';
	import Login from './routes/Login.svelte';
	import SignUp from './routes/SignUp.svelte';
	import ForgotPassword from './routes/ForgotPassword.svelte';
	import {userbaseStore, userStore} from "./stores";
	const userbase = window.userbase;
	window.userbase = null;

	//stores
	$userbaseStore = userbase;
	$userStore = null;

	userbase.init({appId: '5e818c6b-c188-49b4-8ab5-0ae7c08c7cf0'})
		.then((session) => $userStore = session.user);
</script>

<Tailwindcss />

<Router routes = {{
	'/': SignUp,
	'/Login': Login,
	'/ForgotPassword': ForgotPassword
}}/>

