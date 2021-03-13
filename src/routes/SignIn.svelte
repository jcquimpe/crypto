<script>
    import Button from '../components/Button.svelte';
    import Input from '../components/Input.svelte';
    import A from '../components/A.svelte';
    import {userbaseStore, userStore, promiseStore} from '../stores';
    let username, password;
    
    function signin(){
        $promiseStore = $userbaseStore.signIn({username, password})
          .then((user) => $userStore = user);
          
    }
</script>

<form on:submit|preventDefault={signin} >
    <div class="container px-5 py-24 mx-auto flex flex-wrap items-center">
      <div class="lg:w-3/5 md:w-1/2 md:pr-16 lg:pr-0 pr-0">
        <h1 class="title-font font-large text-6xl text-white font-anton">Dominate the blockchain!</h1>
        <p class="leading-relaxed mt-4 text-2xl">The next phase of gaming has the potential to be just as lucrative, and the force behind it is blockchain technology.</p>
      </div>
      <div class="lg:w-2/6 md:w-1/2 bg-gray-800 bg-opacity-50 rounded-lg p-8 flex flex-col md:ml-auto w-full mt-10 md:mt-0">
        
        <div>
          <span class="text-white text-lg font-medium title-font mb-5 pr-24 mr-20">Login</span>
          <A href="#/SignUp" class="">Register</A>
        </div>
        <Input label="Username" bind:value={username} type="text" required/>
        <Input label="Password" bind:value={password} type="password" required/>
        <Button>Login</Button>
      </div>
    </div>
</form>