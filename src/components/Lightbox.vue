<template>
  <div class="lightbox">
    <div class="lightbox__box">
      <div class="lightbox__close" @click="$emit('close-lightbox')">
        <img src="../assets/icons/icon-close.svg" alt="Icon close" />
      </div>
      <div class="gallery">
        <div class="gallery__wrapper">
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
        </div>

        <div class="gallery__tabs flex-between">
          <div
            class="gallery__tab"
            :class="thumb === imgNumbers.imgProductNumber ? 'active' : ''"
            v-for="thumb in imgNumbers.thumbnailNumbers"
            :key="thumb"
            @click="imgNumbers.imgProductNumber = thumb"
          >
            <img
              :src="
                require(`@/assets/images/image-product-${thumb}-thumbnail.jpg`)
              "
              alt="Product Image thumb"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Gallery from './Gallery.vue';
export default {
  components: { Gallery },
  props: {
    imgNumbers: {
      type: Object,
    },
  },
};
</script>

<style lang="scss" scoped>
.lightbox {
  position: fixed;
  inset: 0 0 0 0;
  display: grid;
  place-items: center;
  background: rgba($black, 0.7);
  z-index: 100;

  &__close {
    position: absolute;
    top: -4rem;
    right: 0;
    z-index: 10;

    img {
      width: 2rem;
      height: 2rem;
      filter: brightness(1000%);
    }

    &:hover img {
      filter: none;
    }
  }

  &__box {
    position: relative;
    width: 30vw;

    .gallery {
      &__wrapper {
        position: relative;
      }

      &__img {
        border-radius: 2rem;
        overflow: hidden;
      }

      &__arrow {
        position: absolute;
        top: 50%;
        display: inline-grid;
        place-items: center;
        width: 5rem;
        aspect-ratio: 1;
        background: $white;
        border-radius: 50%;
        cursor: pointer;

        &--prev {
          left: 0;
          transform: translate(-50%, -50%);
        }

        &--next {
          right: 0;
          transform: translate(50%, -50%);
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

        &:hover {
          background: $white;
          border-color: rgba($black, 0.7);

          img {
            opacity: 0.5;
          }
        }
      }

      .active {
        background: $white;
        border-color: $orange;

        img {
          opacity: 0.5;
        }
      }
    }
  }
}
</style>
