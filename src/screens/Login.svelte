<script lang="ts">
  import { useNavigate } from 'svelte-navigator';
  import ROUTES from '../constants/routes';
  import isLoggedIn from '../stores/store';

  const navigate = useNavigate();

  const handleClick = () => {
    isLoggedIn.update(() => true);
    navigate(ROUTES.HOME, { replace: true });
  };
</script>

<div class="container">
  <h1 class="title">You need to login to access our jokes page.</h1>
  <button class="login-btn" on:click={handleClick}>Login</button>
</div>

<style lang="scss">
  @import '../scss/colors';

  .container {
    align-items: center;
    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
  }

  .title {
    font-size: clamp(1.75rem, 2vw, 9rem);
    margin: 2em 0;
    text-align: center;
  }

  .login-btn {
    border: 4px solid $rio-grande;
    font-size: clamp(1.25rem, 1.5vw, 8rem);
    font-weight: 800;
    padding: 1em 2.5em;
    transform: scale(1);
    transition: all 250ms ease-in-out;

    &:hover {
      background-color: $rio-grande;
      color: $cod-gray;
      transform: scale(1.1);
    }
  }
</style>
