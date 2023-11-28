<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start the game</h3>
    <div class="action">
      <button @click="onStart(16)">
        <span>4 x 4</span>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6 x 6</span>
        <span>Normal</span>
      </button>
      <button @click="onStart(64)">
        <span>8 x 8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10 x 10</span>
        <span>Very hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(totalBlocks) {
      this.$emit('onStart', { totalBlocks })
    }
  },
}
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: var(--dark);
  color: var(--light);
}

.screen h1 {
  font-size: 4.5rem;
  text-transform: uppercase;
}

.screen h3 {
  font-size: 2rem;
}

.action {
  display: flex;
  margin-top: 2rem;
}

.action button {
  font: var(--font);
  width: 150px;
  height: 150px;
  background: transparent;
  box-shadow: none;
  border: 1px solid var(--light);
  color: var(--light);
  display: flex;
  flex-direction: column;
  border-radius: 1rem;
  margin: 0 1rem;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}

.action button:hover {
  background-color: var(--light);
  color: var(--dark);
}

.action button span:first-child {
  font-size: 2rem;
}

.action button span:last-child {
  display: block;
  font-size: 1.25rem;
  margin-top: 0.5rem;
}
</style>
