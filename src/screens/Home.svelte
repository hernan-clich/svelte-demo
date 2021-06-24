<main>
  <h1>Hello world!</h1>
  <p>
    Visit the <a href="https://svelte.dev/tutorial">Svelte tutoriasl</a> to learn
    how to build Svelte apps.
  </p>
</main>

<style lang="scss">
  main {
    margin: 0 auto;
    max-width: 240px;
    padding: 1em;
    text-align: center;

    h1 {
      color: #ff3e00;
      font-size: 4em;
      font-weight: 100;
      text-transform: uppercase;
    }
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
