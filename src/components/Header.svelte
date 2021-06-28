<script lang="ts">
  import { onMount } from 'svelte';
  import { Link, useNavigate } from 'svelte-navigator';
  import { fade } from 'svelte/transition';
  import ROUTES from '../constants/routes';
  import isLoggedIn from '../stores/store';

  export let appName: string;
  const navigate = useNavigate();

  let visible = false;

  onMount(() => (visible = true));

  const handleClick = () => {
    isLoggedIn.update(() => false);
    navigate(ROUTES.LOGIN, { replace: true });
  };
</script>

<header class="container">
  {#if visible}
    {#each appName as char, i}
      <span class="logo" in:fade={{ delay: 1000 + i * 150, duration: 350 }}
        >{char}</span
      >
    {/each}
    <nav class="navbar" in:fade={{ delay: 3000, duration: 500 }}>
      {#if $isLoggedIn}
        <div class="auth-nav">
          <Link to={ROUTES.HOME}>Jokes</Link>
          <Link to={ROUTES.ABOUT}>About</Link>
        </div>
        <button class="logout" on:click={handleClick}>Logout</button>
      {:else}
        <div>
          <Link to={ROUTES.LOGIN}>Login</Link>
          <Link to={ROUTES.ABOUT}>About</Link>
        </div>
      {/if}
    </nav>
  {/if}
</header>

<style lang="scss">
  @import '../scss/colors';

  .container {
    align-items: center;
    display: flex;
    padding: 1em;
  }

  .logo {
    font-size: clamp(1.5rem, 2.25vw, 20rem);
    font-style: italic;
    font-weight: 600;
  }

  .navbar {
    align-items: center;
    display: flex;
    flex-grow: 1;
    justify-content: space-between;
    padding-right: 2em;
  }

  .auth-nav {
    display: flex;
    flex-wrap: nowrap;
  }

  :global(a) {
    font-size: clamp(1rem, 1.15vw, 10rem);
    font-style: normal;
    font-weight: 600;
    margin: 0 1em;
    padding: 0.5em;

    &:hover {
      font-style: italic;
    }
  }

  .logout {
    background-color: $rio-grande;
    border: 4px solid $rio-grande;
    color: $cod-gray;
    font-size: clamp(1rem, 1.1vw, 10rem);
    font-style: normal;
    font-weight: 600;
    padding: 0.5em 1em;
    transform: scale(1);
    transition: all 250ms ease-in-out;

    &:hover {
      background-color: $cod-gray;
      color: $rio-grande;
      transform: scale(1.1);
    }
  }
</style>
