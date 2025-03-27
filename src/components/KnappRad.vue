<script setup>
const props = defineProps(['knappar', 'reset'])

const emit = defineEmits(['valdaKnappar'])

import { watch } from 'vue'

// spelarens val
function spelarval(e) {
  let buttons = document.getElementsByClassName('alternativ')
  for (let b of buttons) {
    b.classList.remove('spelarval')
  }
  e.target.classList.add('spelarval')
  emit('valdaKnappar', { spelare: e.target.textContent, dator: datorval() })
}

// datorns val
function datorval() {
  let val = Math.floor(Math.random() * props.knappar.length)
  let buttons = document.getElementsByClassName('alternativ')

  for (let b of buttons) {
    b.classList.remove('datorval')
    b.title = ''
    if (b.textContent == props.knappar[val]) {
      b.classList.add('datorval')
      b.title = 'Datorns val'
    }
  }
  return props.knappar[val]
}

watch(
  () => props.reset,
  () => {
    if (props.reset) {
      let buttons = document.getElementsByClassName('alternativ')
      for (let b of buttons) {
        b.classList.remove('spelarval')
        b.classList.remove('datorval')
        b.title = ''
      }
    }
  }
)
</script>

<template>
  <!-- knapparna -->
  <div class="knapprad">
    <button v-for="knapp in props.knappar" class="alternativ" :key="knapp" @click="spelarval">
      {{ knapp }}
    </button>
  </div>
</template>

<style scoped>
.knapprad {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 1em;
  margin: 2em 0;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

button {
  padding: 0.8em 1.5em;
  font-size: 0.8em;
  background-color: #0a0014;
  border: 3px solid #4d4dff;
  border-radius: 0;
  color: #4d4dff;
  cursor: pointer;
  font-family: 'Press Start 2P', cursive;
  text-transform: uppercase;
  transition: all 0.2s ease;
  box-shadow: 0 0 10px #4d4dff;
  min-width: 150px;
}

button:hover {
  background-color: #4d4dff;
  color: #0a0014;
  transform: scale(1.05);
  box-shadow:
    0 0 15px #4d4dff,
    0 0 30px #8a2be2;
}

button.spelarval {
  background-color: #00ff00;
  border-color: #00ff00;
  color: #0a0014;
  animation: pulseGreen 1s infinite;
  box-shadow:
    0 0 15px #00ff00,
    0 0 30px #00ff00;
}

button.datorval {
  background-color: #ff0000;
  border-color: #ff0000;
  color: #0a0014;
  animation: pulseRed 1s infinite;
  box-shadow:
    0 0 15px #ff0000,
    0 0 30px #ff0000;
}

@keyframes pulseGreen {
  0% {
    transform: scale(1);
    box-shadow:
      0 0 15px #00ff00,
      0 0 30px #00ff00;
  }
  50% {
    transform: scale(1.05);
    box-shadow:
      0 0 20px #00ff00,
      0 0 40px #00ff00;
  }
  100% {
    transform: scale(1);
    box-shadow:
      0 0 15px #00ff00,
      0 0 30px #00ff00;
  }
}

@keyframes pulseRed {
  0% {
    transform: scale(1);
    box-shadow:
      0 0 15px #ff0000,
      0 0 30px #ff0000;
  }
  50% {
    transform: scale(1.05);
    box-shadow:
      0 0 20px #ff0000,
      0 0 40px #ff0000;
  }
  100% {
    transform: scale(1);
    box-shadow:
      0 0 15px #ff0000,
      0 0 30px #ff0000;
  }
}
</style>
