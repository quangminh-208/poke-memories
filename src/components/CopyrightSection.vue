<template>
  <div class="copyright">
    <p>
      This game devloped by Minh Woody in Vue 3 -
      <a href="https://github.com/quangminh-208/poke-memories">view here</a>
    </p>
  </div>
</template>

<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}

.copyright a {
  color: #f4dc26;
}
</style>
