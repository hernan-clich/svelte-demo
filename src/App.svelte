<script lang="ts">
  import { Router, Route } from 'svelte-navigator';
  import { QueryClient, QueryClientProvider } from '@sveltestack/svelte-query';
  import Header from './components/Header.svelte';
  import PrivateRoute from './components/PrivateRoute.svelte';
  import ROUTES from './constants/routes';
  import Home from './screens/Home.svelte';
  import Login from './screens/Login.svelte';
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
      <PrivateRoute path={ROUTES.HOME}>
        <Home />
      </PrivateRoute>
      <Route path={ROUTES.LOGIN}>
        <Login />
      </Route>
      <Route path={ROUTES.ABOUT}>
        <About />
      </Route>
    </div>
  </Router>
</QueryClientProvider>
