<script lang="ts">
  import { Link, Router, Route } from 'svelte-navigator';
  import { QueryClient, QueryClientProvider } from '@sveltestack/svelte-query';
  import Home from './screens/Home.svelte';
  import About from './screens/About/index.svelte';

  const queryClient = new QueryClient({
    defaultOptions: {
      queries: {
        refetchOnWindowFocus: false,
      },
    },
  });
</script>

<QueryClientProvider client={queryClient}>
  <Router>
    <header>
      <Link to="/">Jokes</Link>
      <Link to="/about">About</Link>
    </header>
    <div>
      <Route path="/">
        <Home />
      </Route>
      <Route path="/about">
        <About />
      </Route>
    </div>
  </Router>
</QueryClientProvider>
