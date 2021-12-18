<template>
  <div class="gallery">
    <div class="gallery__img">
      <img
        :src="
          require(`@/assets/images/image-product-${imgNumbers.imgProductNumber}.jpg`)
        "
        alt="Product Image"
        @click="$emit('open-lightbox')"
      />
    </div>
    <div
      class="gallery__arrow gallery__arrow--prev"
      v-if="mobileView"
      @click="
        imgNumbers.imgProductNumber > 1
          ? imgNumbers.imgProductNumber--
          : (imgNumbers.imgProductNumber = 4)
      "
    >
      <svg width="13" height="18" xmlns="http://www.w3.org/2000/svg">
        <path
          d="M11 1 3 9l8 8"
          stroke-width="3"
          fill="none"
          fill-rule="evenodd"
        />
      </svg>
    </div>
    <div
      class="gallery__arrow gallery__arrow--next"
      v-if="mobileView"
      @click="
        imgNumbers.imgProductNumber < 4
          ? imgNumbers.imgProductNumber++
          : (imgNumbers.imgProductNumber = 1)
      "
    >
      <svg width="13" height="18" xmlns="http://www.w3.org/2000/svg">
        <path
          d="m2 1 8 8-8 8"
          stroke-width="3"
          fill="none"
          fill-rule="evenodd"
        />
      </svg>
    </div>
    <div class="gallery__tabs flex-between" v-if="!mobileView">
      <div
        class="gallery__tab"
        :class="thumb === imgNumbers.imgProductNumber ? 'active' : ''"
        v-for="thumb in imgNumbers.thumbnailNumbers"
        :key="thumb"
        @click="imgNumbers.imgProductNumber = thumb"
      >
        <img
          :src="require(`@/assets/images/image-product-${thumb}-thumbnail.jpg`)"
          alt="Product Image thumb"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    mobileView: {
      type: Boolean,
      default: false,
    },
    imgNumbers: {
      type: Object,
    },
  },
};
</script>

<style lang="scss" scoped>
.gallery {
  position: relative;
  width: calc(100% + 4rem);
  margin-left: -2rem;
  margin-top: 3.7rem;

  @include desktop {
    width: 100%;
    flex-basis: 50%;
    margin-left: 0;
    margin-top: 0;
  }

  &__img {
    height: 33rem;
    overflow: hidden;
    cursor: pointer;

    @include desktop {
      height: auto;
      border-radius: 2rem;
    }
  }

  &__arrow {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    display: inline-grid;
    place-items: center;
    width: 3.5rem;
    aspect-ratio: 1;
    background: $white;
    border-radius: 50%;
    cursor: pointer;

    &--prev {
      left: 1rem;
    }

    &--next {
      right: 1rem;
    }

    svg {
      stroke: $very-dark-blue;

      &:hover {
        stroke: $orange;
      }
    }
  }

  &__tabs {
    margin-top: 3rem;
    @include gap-space(3rem);
  }

  &__tab {
    border-radius: 1rem;
    overflow: hidden;
    border: 2px solid transparent;
    cursor: pointer;

    &:hover img {
      opacity: 0.5;
    }
  }

  .active {
    border-color: $orange;

    img {
      opacity: 0.5;
    }
  }
}
</style>
