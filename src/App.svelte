<script>
	import Tailwindcss from './Tailwindcss.svelte';
	import Router from 'svelte-spa-router';
	import Login from './routes/Login.svelte';
	import Register from './routes/Register.svelte';
	import ForgotPassword from './routes/ForgotPassword.svelte';
	
	const userbase = window.userbase;
	delete window.userbase;

	userbase.init({appID: '	5e818c6b-c188-49b4-8ab5-0ae7c08c7cf0'})
</script>

<Tailwindcss />

<Router routes = {{
	'/': Login,
	'/Register': Register,
	'/ForgotPassword': ForgotPassword
}}/>

