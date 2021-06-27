<script lang="ts">
  import { useQuery } from '@sveltestack/svelte-query';
  import { onMount } from 'svelte';
  import Loader from '../components/Loader.svelte';
  import type { Joke } from '../interfaces/jokes';

  const jokesUrl =
    'https://official-joke-api.appspot.com/jokes/programming/ten';
  const queryResult = useQuery<Joke[]>('jokes', () =>
    fetch(jokesUrl).then((res) => res.json())
  );
</script>

<h1 class="title">Jokes</h1>
{#if $queryResult.isLoading}
  <Loader />
{:else if $queryResult.isError}
  <pre
    class="error">
    There was an error fetching the jokes, please try again later
  </pre>
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

<style lang="scss">
  @import '../scss/colors.scss';

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
    background-color: $rio-grande;
    border-top: 0.75rem solid $verdun-green;
    color: $verdun-green;
    clip-path: polygon(
      0% 0%,
      100% 0%,
      100% 75%,
      70% 75%,
      75% 100%,
      60% 75%,
      0% 75%
    );
    display: flex;
    flex-flow: column nowrap;
    justify-content: space-evenly;
    margin: 2rem;
    padding: 2rem 2rem 8rem;
    transform: rotateX(10deg) rotateY(-10deg) scale(1);
    transition: all 250ms;

    &:hover {
      background-color: $aqua-deep;
      border-top: 0.75rem solid $robins-egg-blue;
      color: $alto;
      transform: scale(1.05);
    }
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

  .error {
    color: red;
    font-size: 2rem;
    font-weight: 800;
    text-align: center;
  }

  @media (max-width: 900px) {
    .jokes-wrapper {
      grid-template-columns: 1fr;
    }
  }
</style>
