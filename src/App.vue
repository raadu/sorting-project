<template>
  <div>
    <button @click="showModal = true">Start Sorting</button>

    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <div class="modal-header">
          <h3 class="modal-title">How many people?</h3>
          <button class="close-button" @click="showModal = false">&times;</button>
        </div>
        <p class="modal-body">Enter a number of how many people you want to add to the list.</p>

        <div class="input-container">
          <input type="number" v-model.number="numberOfPeople" min="20" max="100" required />
        </div>

        <div class="modal-buttons">
          <button class="modal-button cancel" @click="showModal = false">Cancel</button>
          <button class="modal-button start" @click="handleStart">Start</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeUnmount } from 'vue'

export default {
  setup() {
    const showModal = ref(false);
    const numberOfPeople = ref(20);
    const people = ref([]);
    const elapsedTime = ref(0);
    const timer = ref(null);

    const handleStart = () => {
      if (numberOfPeople.value >= 20 && numberOfPeople.value <= 100) {
        showModal.value = false;
        generatePeople();
        startTimer();
      } else {
        alert("Please enter a number between 20 and 100");
      }
    };

    const generatePeople = () => {
      const names = ["Alice", "Bob", "Charlie", "David", "Eva", "Frank", "Grace"];
      const emails = ["gmail.com", "yahoo.com", "hotmail.com", "outlook.com"];
      const uniquePotatoCounts = [];

      while (uniquePotatoCounts.length < numberOfPeople.value) {
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

    return {
      showModal,
      numberOfPeople,
      people,
      elapsedTime,
      handleStart,
      generatePeople,
      generateRandomString,
      startTimer,
    };

  }


}
</script>

<style>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  border-radius: 5px;
  width: 300px;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid grey;
  padding: 8px;
}

.modal-title {
  font-size: 16px;
  font-weight: bold;
}

.close-button {
  background: none;
  border: none;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
  color: #333;
}

.close-button:hover {
  color: #ff9800;
}

.modal-body {
  padding: 12px 10px 0px 10px;
  font-size: 12px;
}

.input-container {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
}

.input-container input {
  width: 100%;
  border: 1px solid grey;
  border-radius: 4px;
  outline: none;
  padding: 5px;
  margin: 10px 0;
}

.modal-buttons {
  padding: 10px;
  display: flex;
  gap: 10px;
  justify-content: flex-end;
  border-top: 1px solid grey;
}

.modal-button {
  padding: 8px 16px;
  font-size: 14px;
  font-weight: bold;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.modal-button.cancel {
  background-color: #f5f5f5;
  color: #333;
}

.modal-button.start {
  background-color: #ff9800;
  color: white;
}
</style>
