<template>
  <header class="header container flex-between">
    <div class="header__left flex">
      <div
        class="header__hamburger"
        :class="{ rotate: isNavOpen }"
        v-if="mobileView"
        @click="showNav"
      >
        <img
          v-if="!isNavOpen"
          src="@/assets/icons/icon-menu.svg"
          alt="Hamburger button icon"
        />
        <img
          v-if="isNavOpen"
          src="@/assets/icons/icon-close.svg"
          alt="Hamburger button icon close"
        />
      </div>
      <img class="header__logo" src="@/assets/icons/logo.svg" alt="Logo" />

      <NavMobile :isNavOpen="isNavOpen" />

      <nav class="nav flex" v-if="!mobileView">
        <a href="#" class="nav__link">Collections</a>
        <a href="#" class="nav__link">Men</a>
        <a href="#" class="nav__link">Women</a>
        <a href="#" class="nav__link">About</a>
        <a href="#" class="nav__link">Contact</a>
      </nav>
    </div>

    <div class="header__right flex">
      <div class="header__cart">
        <img src="@/assets/icons/icon-cart.svg" alt="Cart icon" />
        <div class="header__cart--count">3</div>
      </div>
      <div class="header__avatar">
        <img src="@/assets/images/image-avatar.png" alt="Avatar image" />
      </div>
    </div>
  </header>
</template>

<script>
import NavMobile from './NavMobile.vue';

export default {
  components: { NavMobile },
  data() {
    return {
      mobileView: false,
      isNavOpen: false,
    };
  },
  created() {
    window.addEventListener('resize', this.handleView);
    this.handleView();
  },
  methods: {
    handleView() {
      this.mobileView = window.innerWidth <= 768;
    },
    showNav() {
      this.isNavOpen = !this.isNavOpen;
    },
  },
};
</script>

<style lang="scss" scoped>
@import '@/scss/_variables.scss';

.header {
  padding-block: 2rem;

  &__right,
  &__left {
    @include gap-space(2rem);
  }

  &__hamburger {
    cursor: pointer;
    @include smooth-transition(transform);

    z-index: 1000;

    img {
      width: 1.8rem;
    }
  }

  .rotate {
    transform: rotate(180deg);
  }

  // &__logo {}

  &__cart {
    position: relative;
    cursor: pointer;

    &--count {
      position: absolute;
      top: -0.5rem;
      right: -0.5rem;
      padding-inline: 0.5rem;
      font-size: 1rem;
      border-radius: 50%;
      color: $white;
      background: $orange;
    }
  }

  &__avatar {
    width: 3rem;
    display: inline-grid;
    aspect-ratio: 1;
    border-radius: 50%;
    border: 2px solid transparent;
    cursor: pointer;

    &:hover {
      border-color: $orange;
    }
  }
}
</style>
