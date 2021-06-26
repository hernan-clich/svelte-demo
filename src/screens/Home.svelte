<script lang="ts">
  import { useQuery } from '@sveltestack/svelte-query';
  import type { Joke } from '../interfaces/jokes';

  const jokesUrl =
    'https://official-joke-api.appspot.com/jokes/programming/ten';
  const queryResult = useQuery<Joke[]>('jokes', () =>
    fetch(jokesUrl).then((res) => res.json())
  );
</script>

<h1 class="title">Jokes</h1>
{#if $queryResult.isLoading}
  <span>Loading...</span>
{:else if $queryResult.error}
  <span>Error</span>
{:else if $queryResult.data}
  <div class="jokes-wrapper">
    {#each $queryResult.data as joke}
      <ul class="joke-container">
        <li class="setup">{joke.setup}</li>
        <li class="punchline">{joke.punchline}</li>
      </ul>
    {/each}
  </div>
{/if}

<style>
  .title {
    font-size: 3rem;
    text-align: center;
  }

  .jokes-wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }
  .joke-container {
    border: 0.5rem solid rgba(205, 188, 0, 1);
    border-radius: 1rem;
    display: flex;
    flex-flow: column nowrap;
    justify-content: space-evenly;
    margin: 2rem;
    padding: 2rem;
  }

  .setup,
  .punchline {
    list-style: none;
    padding: 1rem 0;
    text-align: center;
  }

  .setup {
    font-size: 1.75rem;
    font-weight: 600;
    text-transform: uppercase;
  }

  .punchline {
    font-size: 1.2rem;
    font-weight: 500;
  }

  @media (max-width: 800px) {
    .jokes-wrapper {
      grid-template-columns: 1fr;
    }
  }
</style>
