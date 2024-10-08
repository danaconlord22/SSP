<script setup>
import { ref } from 'vue'

// spelarens och datorns poäng
const score = ref({ spelare: 0, dator: 0 })
const resultat = ref('Spelet har börjat!') // rätt text vid start

// spelarens val
function spelarval(e) {
  let buttons = document.getElementsByClassName('alternativ')
  for (let b of buttons) {
    b.classList.remove('spelarval')
  }
  e.target.classList.add('spelarval')
  datorval()
  hittaVinnare()
}

// datorns val
function datorval() {
  let val = Math.floor(Math.random() * 3)
  let alternativ = ['Sten', 'Sax', 'Påse']
  let buttons = document.getElementsByClassName('alternativ')

  for (let b of buttons) {
    b.classList.remove('datorval')
    b.title = ''
    if (b.textContent == alternativ[val]) {
      b.classList.add('datorval')
      b.title = 'Datorns val'
    }
  }
}

function hittaVinnare() {
  let buttons = document.getElementsByClassName('alternativ')
  for (let b of buttons) {
    if (b.classList.contains('spelarval')) {
      var spelarval = b.textContent
    }
    if (b.classList.contains('datorval')) {
      var datorval = b.textContent
    }
  }

  if (spelarval == datorval) {
    resultat.value = 'Oavgjort!'
  } else if (
    (spelarval == 'Sten' && datorval == 'Sax') ||
    (spelarval == 'Sax' && datorval == 'Påse') ||
    (spelarval == 'Påse' && datorval == 'Sten')
  ) {
    resultat.value = 'Du vann!'
    score.value.spelare++
  } else {
    resultat.value = 'Du förlorade!'
    score.value.dator++
  }
}

function reset() {
  score.value.spelare = 0
  score.value.dator = 0
  resultat.value = 'Spelet har börjat!' // Reset result message to a default
  let buttons = document.getElementsByClassName('alternativ')
  for (let b of buttons) {
    b.classList.remove('spelarval')
    b.classList.remove('datorval')
  }
}
</script>

<template>
  <!-- rubrik -->
  <header>
    <h1>Sten, Sax, Påse!</h1>
  </header>

  <!-- knapparna -->
  <main>
    <div class="knapprad">
      <button class="alternativ" @click="spelarval">Sten</button>
      <button class="alternativ" @click="spelarval">Sax</button>
      <button class="alternativ" @click="spelarval">Påse</button>
    </div>

    <!-- resultat -->
    <div class="resultat">
      <p id="resultat">{{ resultat }}</p>
    </div>

    <!-- poäng -->
    <div class="score">
      <p>
        <span id="spelare">{{ score.spelare }}</span> -
        <span id="dator">{{ score.dator }}</span>
      </p>
    </div>

    <div class="score">
      <button id="nolla" @click="reset">Nollställ poängen</button>
    </div>
  </main>
</template>

<style scoped>
header {
  text-align: center;
  margin-bottom: 1.2em;
}

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
  justify-content: center;
  gap: 0.6em;
}

.resultat {
  font-size: 1.2em;
  text-align: center;
  margin: 1.2em 0;
}

.score {
  font-size: 1.2em;
  text-align: center;
}

button.spelarval {
  background-color: greenyellow;
}

button.datorval {
  border: red solid 2px;
}

#nolla {
  margin-top: 2em;
  padding: 0.3em 0.6em;
  font-size: 0.8em;
}
</style>
