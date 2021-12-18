<template>
  <div class="cart">
    <h2 class="cart__header">Cart</h2>
    <div class="cart__content">
      <div class="product" v-if="Object.keys(product).length !== 0">
        <div class="product__content flex-between">
          <img class="product__img" :src="product.imgUrl" alt="Product Image" />
          <div class="product__details">
            <p class="product__title">
              {{ product.title.substring(0, 25) + '...' }}
            </p>
            <div class="product__price-group flex">
              <span class="product__price"
                >${{ product.price.new.toFixed(2) }}</span
              >
              <span>x</span>
              <span class="product__counter">{{ product.counter }}</span>
              <span class="product__total"
                >${{ product.total.toFixed(2) }}</span
              >
            </div>
          </div>
          <div class="product__icon" @click="$emit('delete-click')">
            <img src="../assets/icons/icon-delete.svg" alt="Icon delete" />
          </div>
        </div>
        <Button text="Checkout" />
      </div>
      <p class="cart__empty-msg" v-if="Object.keys(product).length === 0">
        Your cart is empty.
      </p>
    </div>
  </div>
</template>

<script>
import Button from './Button.vue';

export default {
  components: { Button },
  props: {
    product: {
      type: Object,
      default: null,
    },
  },
};
</script>

<style lang="scss" scoped>
.cart {
  position: absolute;
  right: 1rem;
  left: 1rem;
  top: calc(100% + 1rem);
  background: $white;
  border-radius: 1rem;
  box-shadow: 1px 20px 20px 10px rgba($black, 0.1);

  @include desktop {
    right: -7rem;
    left: auto;
    top: 100%;
    width: 35rem;
  }

  &__header {
    padding: 2.5rem;
    font-size: 1.8rem;
    font-weight: 700;
    color: $very-dark-blue;
    border-bottom: 1px solid lighten($grayish-blue, 15%);
  }

  &__content {
    position: relative;
    height: 18rem;
    padding: 2.5rem;
  }

  &__empty-msg {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-weight: 700;
  }
}

.product {
  &__content {
    margin-bottom: 2.5rem;
  }

  &__img {
    width: 5rem;
    border-radius: 0.5rem;
  }

  &__price-group {
    @include gap-space(0.5rem);
    line-height: 1.8;
  }

  &__total {
    font-weight: 700;
    color: $very-dark-blue;
  }

  &__icon {
    cursor: pointer;
  }
}
</style>
