<script lang="ts">
  import { useNavigate, useLocation } from 'svelte-navigator';
  import ROUTES from '../constants/routes';
  import isLoggedIn from '../stores/store';

  const navigate = useNavigate();
  const location = useLocation();

  $: if (!$isLoggedIn) {
    navigate(ROUTES.LOGIN, {
      state: { from: $location.pathname },
      replace: true,
    });
  }
</script>

{#if $isLoggedIn}
  <slot />
{/if}
