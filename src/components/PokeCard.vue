<template>
  <div
    class="card"
    :class="{ disabled: isDisabled }"
    :style="{
      height:
        (Math.sqrt(cardsContext.length) < 8
          ? (600 - 16 * 4) / Math.sqrt(cardsContext.length) - 16
          : Math.sqrt(cardsContext.length) < 10
          ? (600 - 16 * 4) / 5.5 - 16
          : (600 - 16 * 4) / 7 - 16) + 'px',
      width:
        (Math.sqrt(cardsContext.length) < 8
          ? (600 - 16 * 4) / Math.sqrt(cardsContext.length) - 16
          : Math.sqrt(cardsContext.length) < 10
          ? (600 - 16 * 4) / 5.5 - 16
          : (600 - 16 * 4) / 7 - 16) + 'px',
      perspective:
        (Math.sqrt(cardsContext.length) < 8
          ? (600 - 16 * 4) / Math.sqrt(cardsContext.length) - 16
          : Math.sqrt(cardsContext.length) < 10
          ? (600 - 16 * 4) / 5.5 - 16
          : (600 - 16 * 4) / 7 - 16) * 2 + 'px',
    }"
  >
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onToggleFlipCard"
    >
      <div class="card__face card__face--front">
        <div
          class="card__content"
          :style="{
            backgroundSize:
              (Math.sqrt(cardsContext.length) < 8
                ? (600 - 16 * 4) / Math.sqrt(cardsContext.length) - 16
                : Math.sqrt(cardsContext.length) < 10
                ? (600 - 16 * 4) / 5.5 - 16
                : (600 - 16 * 4) / 7 - 16) / 2 + 'px ' +
              (Math.sqrt(cardsContext.length) < 8
                ? (600 - 16 * 4) / Math.sqrt(cardsContext.length) - 16
                : Math.sqrt(cardsContext.length) < 10
                ? (600 - 16 * 4) / 5.5 - 16
                : (600 - 16 * 4) / 7 - 16) / 2 + 'px',
          }"
        ></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    card: {
      type: [String, Number, Array, Object],
    },
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      isDisabled: false,
      isFlipped: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      if (this.isDisabled) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) this.$emit("onFlip", this.card);
    },
    onFlipBackCard() {
      this.isFlipped = false;
    },
    onDisableCard() {
      this.isDisabled = true;
    },
  },
};
</script>

<style scoped>
.card {
  display: inline-block;
  margin: 1rem;
}

.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 0.8s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card.disabled .card__inner {
  cursor: default;
}

.card__inner.is-flipped {
  transform: rotateY(-180deg);
}

.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}

.card__face--front .card__content {
  background: url(../assets/images/icon_back.png) no-repeat center center;
  /* background-size: 88px 88px; */
  width: 100%;
  height: 100%;
}

.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}

.card__face--back .card__content {
  background: no-repeat center center;
  background-size: contain;
  width: 100%;
  height: 100%;
}
</style>
