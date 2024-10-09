<script setup>
import { ref } from 'vue'

import KnappRad from './components/KnappRad.vue'

import ResultatRad from './components/ResultatRad.vue'

const knappar = ref(['Sten', 'Sax', 'Påse'])

// spelarens och datorns poäng
const score = ref({ spelare: 0, dator: 0 })
const resultat = ref({})

// ge poäng och visa resultat
function hittaVinnare(valdaKnappar) {
  console.log('Valda knappar:', valdaKnappar)
  let spelare = knappar.value.indexOf(valdaKnappar.spelare)
  let dator = knappar.value.indexOf(valdaKnappar.dator)
  resultat.value = { spelare: spelare, dator: dator }
}

// reset buttons function
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

  <main>
    <KnappRad :knappar="knappar" @valda-knappar="hittaVinnare" />

    <!-- resultat -->
    <ResultatRad :valda-knappar="resultat" />

    <!-- poäng -->
    <div class="score">
      <p>
        <span id="spelare">{{ score.spelare }}</span> -
        <span id="dator">{{ score.dator }}</span>
      </p>
    </div>

    <!-- nollställ knapp -->
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

.score {
  font-size: 1.2em;
  text-align: center;
}

#nolla {
  margin-top: 2em;
  padding: 0.3em 0.6em;
  font-size: 0.8em;
}
</style>
