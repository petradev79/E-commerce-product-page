<template>
  <header class="container header flex-between">
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
      <img src="@/assets/icons/logo.svg" alt="Logo" />

      <NavMobile :isNavOpen="isNavOpen" />
      <NavDesktop v-if="!mobileView" />
    </div>

    <div class="header__right flex">
      <div class="header__cart-btn" @click="showCart">
        <svg width="22" height="20" xmlns="http://www.w3.org/2000/svg">
          <path
            d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z"
            fill-rule="nonzero"
          />
        </svg>
        <div
          v-if="Object.keys(product).length !== 0"
          class="header__cart-btn--count"
        >
          {{ product.counter }}
        </div>
      </div>
      <div class="header__avatar">
        <img src="@/assets/images/image-avatar.png" alt="Avatar image" />
      </div>
    </div>
    <Cart
      v-if="isCartOpen"
      :product="product"
      @delete-click="$emit('delete-product')"
    />
  </header>
</template>

<script>
import NavMobile from './NavMobile.vue';
import NavDesktop from './NavDesktop.vue';
import Cart from './Cart.vue';

export default {
  components: { NavMobile, NavDesktop, Cart },
  props: {
    mobileView: {
      type: Boolean,
      default: false,
    },
    product: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      isNavOpen: false,
      isCartOpen: false,
    };
  },
  methods: {
    showNav() {
      this.isNavOpen = !this.isNavOpen;
    },
    showCart() {
      this.isCartOpen = !this.isCartOpen;
    },
  },
};
</script>

<style lang="scss" scoped>
.header {
  position: fixed;
  top: 0;
  width: 100%;
  padding-block: 2rem;
  background: $white;
  z-index: 10;

  @include desktop {
    position: relative;
    padding-block: 0;
    border-bottom: 1px solid lighten($grayish-blue, 15%);
  }

  &__right,
  &__left {
    @include gap-space(2rem);

    @include desktop {
      @include gap-space(5rem);
    }
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

  &__cart-btn {
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

    svg {
      fill: $dark-grayish-blue;
    }

    svg:hover {
      fill: $very-dark-blue;
    }
  }

  &__avatar {
    width: 3rem;
    display: inline-grid;
    aspect-ratio: 1;
    border-radius: 50%;
    border: 2px solid transparent;
    cursor: pointer;

    @include desktop {
      width: 5rem;
    }

    &:hover {
      border-color: $orange;
    }
  }
}
</style>
