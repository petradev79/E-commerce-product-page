<template>
  <transition name="fade">
    <div class="overlay" v-show="isNavOpen"></div>
  </transition>
  <transition name="slide">
    <nav class="nav flex" v-show="isNavOpen">
      <a href="#">Collections</a>
      <a href="#">Men</a>
      <a href="#">Women</a>
      <a href="#">About</a>
      <a href="#">Contact</a>
    </nav>
  </transition>
</template>

<script>
export default {
  props: {
    isNavOpen: {
      type: Boolean,
      defoult: false,
    },
  },
};
</script>

<style lang="scss" scoped>
.overlay {
  position: fixed;
  inset: 0 0 0 0;
  background: rgba($black, 0.5);
  z-index: 100;
}

.nav {
  flex-direction: column;
  align-items: flex-start;
  @include gap-space(2.5rem);
  position: fixed;
  inset: 0 30% 0 0;
  padding-top: 10rem;
  padding-left: 2rem;
  background: $white;
  z-index: 100;

  a {
    font-size: 2rem;
    font-weight: bold;
    color: $very-dark-blue;
  }
}

// modal-overlay fade in/out transition
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.fade-enter-active,
.fade-leave-active {
  @include smooth-transition(opacity);
}

// mobile navigation slide in/out transition
.slide-enter-from,
.slide-leave-to {
  transform: translateX(-100%);
}
.slide-enter-active,
.slide-leave-active {
  @include smooth-transition(transform);
}
</style>
