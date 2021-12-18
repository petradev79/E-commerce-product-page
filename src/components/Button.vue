<template>
  <button class="btn flex-center" @click="$emit('btn-click')">
    <img v-if="imgUrl" :src="imgUrl" alt="Cart Icon" />
    {{ text }}
  </button>
</template>

<script>
export default {
  props: {
    text: String,
    imgUrl: String,
  },
};
</script>

<style lang="scss" scoped>
.btn {
  width: 100%;
  padding: 2rem;
  font-size: inherit;
  font-weight: 700;
  background: $orange;
  color: $white;
  border: none;
  border-radius: 1rem;
  cursor: pointer;

  &:hover {
    opacity: 0.5;
  }

  img {
    height: 1.5rem;
    filter: brightness(500%);
  }
}
</style>
