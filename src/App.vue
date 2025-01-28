<template>
  <div>
    <button @click="showModal = true">Start Sorting</button>

    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <h3>How many people?</h3>
        <p>Enter a number of how many people you want to add to the list</p>

        <input type="number" v-model.number="numberOfPeople" min="20" max="100" required />

        <div class="modal-buttons">
          <button @click="showModal = false">Cancel</button>
          <button @click="handleStart">Start</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showModal: false,
      numberOfPeople: 20,
    }
  },
  methods: {
    handleStart() {
      if (this.numberOfPeople >= 20 && this.numberOfPeople <= 100) {
        // Add your sorting logic here
        console.log(`Starting sorting with ${this.numberOfPeople} people`)
        this.showModal = false
      } else {
        alert('Please enter a number between 20 and 100')
      }
    },
  },
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
  padding: 20px;
  border-radius: 5px;
  width: 300px;
}

.modal-buttons {
  margin-top: 20px;
  display: flex;
  gap: 10px;
  justify-content: flex-end;
}

input[type='number'] {
  width: 100%;
  padding: 5px;
  margin: 10px 0;
}
</style>
