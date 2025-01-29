<template>
  <div>
    <button class="start-sorting-button" @click="showModal = true">Start Sorting</button>

    <ModalComponent :showModal="showModal" @close-modal="showModal = false" @start-sorting="handleStartSorting" />
  </div>
</template>

<script setup>
import { ref, onBeforeUnmount } from 'vue';
import ModalComponent from './components/ModalComponent.vue';

const showModal = ref(false);
const people = ref([]);
const elapsedTime = ref(0);
const timer = ref(null);

const handleStartSorting = (numberOfPeople) => {
  generatePeople(numberOfPeople);
  startTimer();
};

const generatePeople = (numberOfPeople) => {
  const names = ["Alice", "Bob", "Charlie", "David", "Eva", "Frank", "Grace"];
  const emails = ["gmail.com", "yahoo.com", "hotmail.com", "outlook.com"];
  const uniquePotatoCounts = [];

  while (uniquePotatoCounts.length < numberOfPeople) {
    const randomPotatoCount = Math.floor(Math.random() * 1000) + 1;
    if (!uniquePotatoCounts.includes(randomPotatoCount)) {
      uniquePotatoCounts.push(randomPotatoCount);
    }
  }

  people.value = uniquePotatoCounts.map((potatoCount, index) => ({
    id: index + 1,
    name: `${names[Math.floor(Math.random() * names.length)]} ${generateRandomString()}`,
    email: `${generateRandomString()}@${emails[Math.floor(Math.random() * emails.length)]}`,
    potatoes: potatoCount,
  }));

  console.log("Generated People:", people.value);
};

const generateRandomString = () => {
  return Math.random().toString(36).substring(7);
};

const startTimer = () => {
  elapsedTime.value = 0;
  if (timer.value) clearInterval(timer.value);
  timer.value = setInterval(() => {
    elapsedTime.value++;
  }, 1000);
};

onBeforeUnmount(() => {
  if (timer.value) clearInterval(timer.value);
});

</script>

<style>
.start-sorting-button {
  background-color: #ff9800;
  color: white;
  padding: 5px;
}
</style>
