<script setup>
// Ta emot props från förälderkomponenten
const props = defineProps(['knappar', 'reset'])

// Skapa emit för att skicka data till föräldern
const emit = defineEmits(['valdaKnappar'])

import { watch } from 'vue'

// Hantera spelarens val av knapp
function spelarval(e) {
  let buttons = document.getElementsByClassName('alternativ')
  for (let b of buttons) {
    b.classList.remove('spelarval')
  }
  e.target.classList.add('spelarval')
  emit('valdaKnappar', { spelare: e.target.textContent, dator: datorval() })
}

// Slumpa fram datorns val
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

// Övervaka reset-prop för att återställa knapparnas utseende
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
button {
  padding: 0.6em 1.2em;
  font-size: 1.2em;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  border-radius: 5px;
  cursor: pointer;
}

.knapprad {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.6em;
}

.alternativ {
  flex: 1 1 calc(11.11% - 0.6em); /* 11.11% width to fit 9 items per row */
  box-sizing: border-box;
}

button.spelarval {
  background-color: greenyellow;
}

button.datorval {
  border: red solid 2px;
}
</style>
