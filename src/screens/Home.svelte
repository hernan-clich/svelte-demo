<script lang="ts">
  import { fade } from 'svelte/transition';
  import { useQuery } from '@sveltestack/svelte-query';
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
  <p class="error">
    There was an error fetching the jokes, please try again later
  </p>
{:else if $queryResult.data}
  <div class="jokes-wrapper">
    {#each $queryResult.data as joke}
      <ul class="joke-container" in:fade>
        <li class="setup">{joke.setup}</li>
        <li class="punchline">{joke.punchline}</li>
      </ul>
    {/each}
  </div>
{/if}

<style lang="scss">
  @import '../scss/colors.scss';

  .title {
    font-size: clamp(2.25rem, 2.75vw, 25rem);
    text-align: center;
  }

  .jokes-wrapper {
    display: grid;
    grid-gap: 2em;
    grid-template-columns: repeat(auto-fill, minmax(min(550px, 100%), 2fr));
    padding: 0 2em;
  }
  .joke-container {
    background-color: $rio-grande;
    border-top: 0.75em solid $verdun-green;
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
    margin: 2em;
    padding: 2em 2em 8em;
    transform: rotateX(10deg) rotateY(-10deg) scale(1);
    transition: all 250ms;

    &:hover {
      background-color: $aqua-deep;
      border-top: 0.75em solid $robins-egg-blue;
      color: $alto;
      transform: scale(1.05);
    }
  }

  .setup,
  .punchline {
    list-style: none;
    padding: 1em 0;
    text-align: center;
  }

  .setup {
    font-size: clamp(1.25rem, 1.5vw, 10rem);
    font-weight: 600;
    text-transform: uppercase;
  }

  .punchline {
    font-size: clamp(1.1rem, 1.2vw, 9rem);
    font-weight: 500;
    padding-bottom: 1.5rem;
  }

  .error {
    color: red;
    font-size: clamp(1.5rem, 1.75vw, 9rem);
    font-weight: 800;
    text-align: center;
  }
</style>
