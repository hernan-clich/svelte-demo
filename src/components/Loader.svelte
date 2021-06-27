<div class="loader" />

<style lang="scss">
  @import '../scss/colors.scss';

  .loader {
    animation: spin 2s linear infinite;
    border: 12px solid $scorpion;
    border-radius: 50%;
    border-top: 12px solid $rio-grande;
    height: 90px;
    margin: 15vh auto;
    width: 90px;

    @keyframes spin {
      0% {
        transform: rotate(0deg);
      }
      100% {
        transform: rotate(360deg);
      }
    }
  }
</style>
