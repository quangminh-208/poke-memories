<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width:
          (Math.sqrt(cardsContext.length) < 8
            ? ((600 - 16 * 4) / Math.sqrt(cardsContext.length) - 16 + 16 * 2) *
              Math.sqrt(cardsContext.length)
            : Math.sqrt(cardsContext.length) < 10
            ? ((600 - 16 * 4) / 5.5 - 16 + 16 * 2) * (cardsContext.length / 4.8)
            : ((600 - 16 * 4) / 7 - 16 + 16 * 2) * (cardsContext.length / 6.5)) +
          'px',
      }"
    >
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        ref="cardRef"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardsContext="cardsContext"
        @onFlip="onCheckRule($event)"
      />
      <result-screen v-if="statusMatch == true" />
    </div>
  </div>
</template>

<script>
import CardFlip from "./PokeCard.vue";
import ResultScreen from "./ResultScreen.vue";

export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
    ResultScreen,
  },
  data() {
    return {
      rules: [],
      isFinished: false,
    };
  },
  methods: {
    onCheckRule(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value &&
        this.rules[0].index !== this.rules[1].index
      ) {
        // Add class 'disabled' to component 'Card'
        this.$refs.cardRef[this.rules[0].index].onDisableCard();
        this.$refs.cardRef[this.rules[1].index].onDisableCard();

        // Reset rules
        this.rules = [];

        // 
        const disabledElements = document.querySelectorAll(
          ".screen .card.disabled"
        );
        if (
          disabledElements &&
          disabledElements.length === this.cardsContext.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          // Flip back card
          this.$refs.cardRef[this.rules[0].index].onFlipBackCard();
          this.$refs.cardRef[this.rules[1].index].onFlipBackCard();
          // Reset rules
          this.rules = [];
        }, 600);
      } else return false;
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}

.screen__inner {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 2rem auto;
}
</style>
