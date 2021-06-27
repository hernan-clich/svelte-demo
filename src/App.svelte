<script lang="ts">
  import { Router, Route } from 'svelte-navigator';
  import { QueryClient, QueryClientProvider } from '@sveltestack/svelte-query';
  import Header from './components/Header.svelte';
  import ROUTES from './constants/routes';
  import Home from './screens/Home.svelte';
  import About from './screens/About/index.svelte';

  const queryClient = new QueryClient({
    defaultOptions: {
      queries: {
        refetchOnWindowFocus: false,
      },
    },
  });

  let appName = '<dev_jokes/>';
</script>

<QueryClientProvider client={queryClient}>
  <Router>
    <Header {appName} />
    <div>
      <Route path={ROUTES.HOME}>
        <Home />
      </Route>
      <Route path={ROUTES.ABOUT}>
        <About />
      </Route>
    </div>
  </Router>
</QueryClientProvider>
