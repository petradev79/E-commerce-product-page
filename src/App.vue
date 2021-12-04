<template>
  <p>
    Collections Men Women About Contact Sneaker Company Fall Limited Edition
    Sneakers These low-profile sneakers are your perfect casual wear companion.
    Featuring a durable rubber outer sole, they’ll withstand everything the
    weather can offer. $125.00 50% $250.00 0 Add to cart Challenge by Frontend
    Mentor. Coded by Your Name Here.
  </p>
</template>

<script>
export default {
  name: 'App',
  components: {},
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@400;700&display=swap');

// ## Colors

// ### Primary

// - Orange: hsl(26, 100%, 55%)
// - Pale orange: hsl(25, 100%, 94%)

// ### Neutral

// - Very vark blue: hsl(220, 13%, 13%)
// - Dark grayish blue: hsl(219, 9%, 45%)
// - Grayish blue: hsl(220, 14%, 75%)
// - Light grayish blue: hsl(223, 64%, 98%)
// - White: hsl(0, 0%, 100%)
// - Black (with 75% opacity for lightbox background): hsl(0, 0%, 0%)

// Users should be able to:

// - View the optimal layout for the site depending on their device's screen size
// - See hover states for all interactive elements on the page
// - Open a lightbox gallery by clicking on the large product image
// - Switch the large product image by clicking on the small thumbnail images
// - Add items to the cart
// - View the cart and remove items from it

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 62.5%;
}

body {
  font-family: 'Kumbh Sans', sans-serif;
  font-size: 1.6rem;
  font-weight: 400;
  // line-height: 1.5;
  // letter-spacing: 0.5px;
  color: hsl(219, 9%, 45%);
  // background-color: $color-dark;
}

a {
  text-decoration: none;
}

img {
  max-width: 100%;
}

// Remove all animations for people that prefer not to see them
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
</style>
