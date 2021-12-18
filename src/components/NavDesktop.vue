<template>
  <nav class="nav-desktop">
    <a href="#">Collections</a>
    <a href="#">Men</a>
    <a href="#">Women</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
  </nav>
</template>

<style lang="scss" scoped>
.nav-desktop {
  display: flex;
  @include gap-space(3rem);

  a {
    padding-block: 4rem;
    color: inherit;
    border-bottom: 3px solid transparent;

    &:hover {
      color: $very-dark-blue;
      border-bottom-color: $orange;
    }
  }
}
</style>
