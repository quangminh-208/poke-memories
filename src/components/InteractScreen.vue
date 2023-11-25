<template>
  <div class="screen">
    <card-flip
      v-for="(card, index) in cardsContext"
      :key="index"
      ref="cardRef"
      :imgBackFaceUrl="`images/${card}.png`"
      :card="{ index, value: card }"
      @onFlip="onCheckRule($event)"
    />
    <result-screen v-if="statusMatch == true" />
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
        console.log("Right");
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
        console.log("Wrong");
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
