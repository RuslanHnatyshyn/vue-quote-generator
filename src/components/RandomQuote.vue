<script setup>
import { ref } from "vue";
import Loader from "./Loader.vue";
import QuoteHistory from "./QuoteHistory.vue";

const quote = ref("");
const author = ref("");
const isLoading = ref(false);
const errorMessage = ref("");
const isShowHistory = ref(false);
const quoteHistory = ref([]);

async function getRandomQuote() {
  isLoading.value = true;
  errorMessage.value = "";

  try {
    const response = await fetch(
      `https://api.codetabs.com/v1/proxy?quest=https://zenquotes.io/api/random`
    );

    const data = await response.json();
    quote.value = data[0].q;
    author.value = data[0].a;

    quoteHistory.value.push({ quote: quote.value, author: author.value });
  } catch (error) {
    console.error("Error loading quote:", error);
    errorMessage.value = "Error loading quote. Please try again later";
  } finally {
    isLoading.value = false;
  }
}

function toggleHistory() {
  isShowHistory.value = !isShowHistory.value;
}

getRandomQuote();
</script>

<template>
  <div class="quote-container">
    <Loader v-if="isLoading" message="Fetching a new quote..." />
    <h2 v-else>{{ quote }}</h2>
    <p v-if="author && !isLoading">{{ author }}</p>
    <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
    <div class="buttons-wrapper">
      <button @click="getRandomQuote" :disabled="isLoading">New Quote</button>
      <button @click="toggleHistory">History</button>
    </div>

    <QuoteHistory
      v-if="isShowHistory"
      :history="quoteHistory"
      @close="toggleHistory"
    />
  </div>
</template>

<style scoped>
.error-message {
  color: #f00000;
  font-weight: 700;
  margin: 10px auto;
}

.buttons-wrapper {
  display: flex;
  justify-content: center;
  gap: 5vw;
  flex-wrap: wrap;
}
</style>
