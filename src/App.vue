<template>
  <main-screen
    v-if="statusMatch == 'defaulf'"
    @onStart="onHandlleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch == 'match'"
    :cardsContext="settings.cardsContext"
    @onFinish="onGetResult"
  />
  <result-screen v-if="statusMatch == 'result'" :timer="timer" @onStartAgain="statusMatch = 'defaulf'"/>
  <copyright-section />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import CopyrightSection from "./components/CopyrightSection.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";

import { shuffled } from "./utils/array.js";

export default {
  name: "App",
  components: {
    MainScreen,
    CopyrightSection,
    InteractScreen,
    ResultScreen,
  },
  data() {
    return {
      settings: {
        totalBlocks: 0,
        cardsContext: [],
        startAt: null,
      },
      statusMatch: "defaulf",
      timer: 0,
    };
  },
  methods: {
    onHandlleBeforeStart(config) {
      console.log("Running handle before start...", config);
      this.settings.totalBlocks = config.totalBlocks;

      const firstCard = Array.from(
        { length: this.settings.totalBlocks / 2 },
        (_, i) => i + 1
      );
      const secoundCards = [...firstCard];
      const cards = [...firstCard, ...secoundCards];
      this.settings.cardsContext = shuffled(shuffled(shuffled(cards)));
      this.settings.startAt = new Date().getTime();
      console.log(this.settings.cardsContext);

      // Data ready
      this.statusMatch = "match";
    },
    onGetResult() {
      // Get timer
      this.timer = new Date().getTime() - this.settings.startAt;

      //  Switch to result component
      this.statusMatch = "result";
    },
  },
};
</script>
