<template>
  <div v-if="history.length" class="modal-overlay">
    <div @click.stop class="modal-content">
      <h2 class="modal-title">Quote History</h2>
      <ul>
        <li v-for="(item, index) in history" :key="index" class="modal-item">
          <p class="modal-quote">"{{ item.quote }}"</p>
          <p class="modal-author">{{ item.author }}</p>
        </li>
      </ul>
      <button @click="$emit('close')" class="modal-close-btn">Close</button>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

defineProps({
  history: {
    type: Array,
    required: true,
  },
});
</script>

<style scoped>
h2 {
  margin-bottom: 10px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 5px 0;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: black;

}

.modal-title {
  color: black;
}

.modal-content {
  background: white;
  color: #41b883;
  padding: 20px;
  max-width: 500px;
  margin: 0 auto;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
  height: 100%;
  overflow-y: auto;
}

.modal-item {
  background-color: darkgrey;
  border-radius: 5px;
  margin-top: 2rem;
  padding: 5px;
  color: black;
}

.modal-quote {
  font-size: 1.5em;
}

.modal-author {
  font-size: 1em;
}

.modal-close-btn {
  transition: all ease 0.5s;
  margin-bottom: 50px;
  width: 100%;
}
.modal-close-btn:hover {
  transform: scale(1.03);
  background-color: dimgrey;
  color: black;
}
</style>
