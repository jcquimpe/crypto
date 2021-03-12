<script>
    import Button from '../components/Button.svelte';
    import Input from '../components/Input.svelte';
    import {userbaseStore, userStore} from '../stores';
    let username, password, email;
    
    function signup(){
        $userbaseStore.signUp({username, password, email})
          .then((user) => $userStore = user);
    }
</script>

<form on:submit|preventDefault={signup} 
class="text-gray-400 bg-gray-500 body-font" style="
background-image: url('../../bg2.jpg');
background-repeat: no-repat;
background-size: cover;
background-blend-mode: multiply;">
    <div class="container px-5 py-24 mx-auto flex flex-wrap items-center">
      <div class="lg:w-3/5 md:w-1/2 md:pr-16 lg:pr-0 pr-0">
        <h1 class="title-font font-large text-6xl text-white font-anton">Dominate the blockchain!</h1>
        <p class="leading-relaxed mt-4 text-2xl">The next phase of gaming has the potential to be just as lucrative, and the force behind it is blockchain technology.</p>
      </div>
      <div class="lg:w-2/6 md:w-1/2 bg-gray-800 bg-opacity-50 rounded-lg p-8 flex flex-col md:ml-auto w-full mt-10 md:mt-0">
        <h2 class="text-white text-lg font-medium title-font mb-5">Sign Up</h2>
        <Input label="Username" bind:value={username} type="text" required/>
        <Input label="Password" bind:value={password} type="password" required/>
        <Input label="Email" bind:value={email} type="email" required/>
        <Button>Sign Up</Button>
        <p class="text-xs mt-3">Literally you probably haven't heard of them jean shorts.</p>
      </div>
    </div>
</form>