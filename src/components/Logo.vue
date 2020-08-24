<template>
  <div class="logo">
    <h1 class="logo__title">
      ilevel
    </h1>
    <h2 class="logo__subtitle">
      web solutions
    </h2>
  </div>
</template>

<script>
export default {
  name: "Logo"
}
</script>

<style lang="scss" scoped>
  .logo {

    &__title,
    &__subtitle {
      margin: 0;
    }

    &__title {
      font-size: 100px;

      &::after {
        content: ".";
        color: rgb(50, 123, 246);
      }
    }

    &__subtitle {
      font-size: 45px;
    }
  }
</style>