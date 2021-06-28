<script lang="ts">
  import { Route } from 'svelte-navigator';
  import PrivateRouteGuard from './PrivateRouteGuard.svelte';

  export let path: string;
</script>

<Route {path} let:params let:location let:navigate>
  <PrivateRouteGuard>
    <slot {params} {location} {navigate} />
  </PrivateRouteGuard>
</Route>
