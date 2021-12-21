<template>
  <Header
    :mobileView="mobileView"
    :product="cartProduct"
    @delete-product="deleteFromCart"
  />
  <main class="main container">
    <Gallery
      :mobileView="mobileView"
      :imgNumbers="imgNumbers"
      @open-lightbox="
        !mobileView ? (showLightbox = true) : (showLightbox = false)
      "
    />
    <Product :product="product" @add-product="addToCart" />
  </main>
  <p class="copyright">
    Challenge by <span>Frontend Mentor</span>. Coded by
    <span>Ivan Petrović</span>.
  </p>
  <transition name="show">
    <Lightbox
      v-if="showLightbox"
      :imgNumbers="imgNumbers"
      @close-lightbox="showLightbox = false"
    />
  </transition>
</template>

<script>
import Header from '@/components/Header.vue';
import Gallery from '@/components/Gallery.vue';
import Product from '@/components/Product.vue';
import Lightbox from '@/components/Lightbox.vue';

export default {
  name: 'App',
  components: { Header, Gallery, Product, Lightbox },
  data() {
    return {
      mobileView: false,
      showLightbox: false,
      imgNumbers: {
        imgProductNumber: 1,
        thumbnailNumbers: [1, 2, 3, 4],
      },
      product: {
        title: 'Fall Limited Edition Sneakers',
        imgUrl: require('@/assets/images/image-product-1-thumbnail.jpg'),
        price: {
          old: 250,
          discount: 50,
          new: 0,
        },
        counter: 0,
      },
      cartProduct: {},
    };
  },
  created() {
    window.addEventListener('resize', this.handleView);
    this.handleView();
    this.product.price.new = this.getNewPrice();
  },
  methods: {
    handleView() {
      this.mobileView = window.innerWidth <= 768;
    },
    getNewPrice() {
      return (this.product.price.discount / 100) * this.product.price.old;
    },
    getTotal(price, counter) {
      return price * counter;
    },
    addToCart(product) {
      if (product.counter !== 0) {
        if (Object.keys(this.cartProduct).length === 0) {
          this.cartProduct = { ...product };
        } else {
          this.cartProduct.counter = this.cartProduct.counter + product.counter;
        }
        this.cartProduct.total = this.getTotal(
          this.cartProduct.price.new,
          this.cartProduct.counter
        );
        this.product.counter = 0;
      }
    },
    deleteFromCart() {
      if (this.cartProduct.counter > 1) {
        this.cartProduct.counter--;
      } else {
        this.cartProduct = {};
      }
    },
  },
};
</script>

<style lang="scss">
.main {
  @include desktop {
    display: flex;
    align-items: center;
    gap: 12rem;
    margin-top: 10rem;
    padding-inline: 5rem;
  }
}

.copyright {
  padding: 2rem;
  text-align: center;
  line-height: 1.6;

  span {
    font-weight: 700;
    color: $orange;
  }

  
}

// lightbox show in/out transition
.show-enter-from,
.show-leave-to {
  opacity: 0;
}
.show-enter-active,
.show-leave-active {
  @include smooth-transition(opacity, 0.3s);
}
</style>
