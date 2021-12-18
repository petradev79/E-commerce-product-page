<template>
  <div class="product">
    <section>
      <h1 class="product__company">Sneaker Company</h1>
      <h2 class="product__title">{{ product.title }}</h2>
      <p class="product__description">
        These low-profile sneakers are your perfect casual wear companion.
        Featuring a durable rubber outer sole, they'll withstand everything the
        weather can offer.
      </p>
    </section>
    <section class="product__cta">
      <div class="price flex-between">
        <div class="price__group flex">
          <span class="price__new">${{ product.price.new.toFixed(2) }}</span>
          <span class="price__discount">{{ product.price.discount }}%</span>
        </div>
        <span class="price__old">${{ product.price.old.toFixed(2) }}</span>
      </div>
      <div class="add-to-cart">
        <div class="add-to-cart__counter flex-between">
          <img
            src="@/assets/icons/icon-minus.svg"
            alt="Icon minus"
            @click="
              product.counter > 0 ? product.counter-- : (product.counter = 0)
            "
          />
          <span>{{ product.counter }}</span>
          <img
            src="@/assets/icons/icon-plus.svg"
            alt="Icon plus"
            @click="product.counter++"
          />
        </div>
        <Button
          text="Add to cart"
          :imgUrl="require('@/assets/icons/icon-cart.svg')"
          @btn-click="$emit('add-product', product)"
        />
      </div>
    </section>
  </div>
</template>

<script>
import Button from './Button.vue';

export default {
  components: { Button },
  props: {
    product: {
      type: Object,
    },
  },
};
</script>

<style lang="scss" scoped>
.product {
  margin-block: 2rem;
  flex-basis: 50%;

  @include desktop {
    margin-top: 0;
  }

  &__company {
    text-transform: uppercase;
    font-size: 1.2rem;
    letter-spacing: 2px;
    color: $orange;

    @include desktop {
      font-size: 1.4rem;
    }
  }

  &__title {
    margin-block: 1.5rem;
    font-size: 3rem;
    line-height: 1.2;
    color: $very-dark-blue;

    @include desktop {
      font-size: 4.5rem;
    }
  }

  &__description {
    font-size: 1.45rem;
    line-height: 1.6;
    color: $dark-grayish-blue;

    @include desktop {
      font-size: 1.6rem;
    }
  }

  &__cta {
    margin-top: 2.5rem;
  }
}

.price {
  @include desktop {
    display: block;
  }

  &__group {
    @include gap-space(2rem);
    @include desktop {
      margin-bottom: 1rem;
    }
  }

  &__new {
    font-size: 3rem;
    font-weight: 700;
    color: $very-dark-blue;
  }

  &__discount {
    padding: 0.3rem 0.7rem;
    font-weight: 700;
    background: $pale-orange;
    color: $orange;
    border-radius: 2px;
  }

  &__old {
    text-decoration: line-through;
    font-weight: 700;
    color: $grayish-blue;
  }
}

.add-to-cart {
  @include desktop {
    display: flex;
    align-items: center;
    @include gap-space(2rem);
    margin-top: 2rem;
  }

  &__counter {
    @include gap-space(2rem);
    margin-block: 2rem;
    padding: 1rem;
    font-weight: 700;
    background: $light-grayish-blue;
    border-radius: 1rem;
    color: $very-dark-blue;

    @include desktop {
      width: 25rem;
    }

    img {
      padding: 1rem;
      cursor: pointer;

      &:hover {
        opacity: 0.5;
      }
    }
  }
}
</style>
