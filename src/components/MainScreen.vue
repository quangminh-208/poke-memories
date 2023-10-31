<template>
  <div class="sreen">
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
