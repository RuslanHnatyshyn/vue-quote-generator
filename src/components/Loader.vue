<template>
  <div class="loader">
    <p>{{ message }}</p>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

defineProps({
  message: {
    type: String,
    default: "Loading...",
  },
});
</script>

<style scoped>
.loader {
  font-size: 1.2em;
  color: #41B883;
  text-align: center;
  margin: 20px 0px;
}
</style>
