<script lang="ts">
  import { onMount } from 'svelte';
  import { Link } from 'svelte-navigator';
  import { fade } from 'svelte/transition';
  import ROUTES from '../constants/routes';

  export let appName: string;

  let visible = false;

  onMount(() => (visible = true));
</script>

<header class="container">
  {#if visible}
    {#each appName as char, i}
      <span class="logo" in:fade={{ delay: 1000 + i * 150, duration: 350 }}
        >{char}</span
      >
    {/each}
    <div in:fade={{ delay: 3000, duration: 500 }}>
      <Link to={ROUTES.HOME}>Jokes</Link>
      <Link to={ROUTES.ABOUT}>About</Link>
    </div>
  {/if}
</header>

<style lang="scss">
  .container {
    align-items: center;
    display: flex;
    padding: 1em;
  }

  .logo {
    font-size: 2.5rem;
    font-style: italic;
    font-weight: 600;
  }

  :global(a) {
    font-size: 1.25rem;
    font-style: normal;
    font-weight: 600;
    margin: 0 1em;
    padding: 0.5em;

    &:hover {
      font-style: italic;
    }
  }
</style>
