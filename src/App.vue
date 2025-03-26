<script setup>
import { ref } from 'vue'

import KnappRad from './components/KnappRad.vue'

import ResultatRad from './components/ResultatRad.vue'
import PoangRad from './components/PoangRad.vue'

const knappar = ref(['Sten', 'Sax', 'Påse'])

// const
const resultat = ref({})
const vinnare = ref('')

const reset = ref(true)

// ge poäng och visa resultat
function hittaVinnare(valdaKnappar) {
  reset.value = false
  vinnare.value = ''
  console.log('Valda knappar:', valdaKnappar)
  let spelare = knappar.value.indexOf(valdaKnappar.spelare)
  let dator = knappar.value.indexOf(valdaKnappar.dator)
  resultat.value = { spelare: spelare, dator: dator }
}

function raknaPoang(v) {
  vinnare.value = v
}
</script>

<template>
  <!-- rubrik -->
  <header>
    <h1>Sten, Sax, Påse!</h1>
  </header>

  <main>
    <KnappRad :knappar="knappar" @valda-knappar="hittaVinnare" :reset="reset" />

    <!-- resultat -->
    <ResultatRad :valda-knappar="resultat" @vinnare="raknaPoang" :reset="reset" />

    <!-- poäng -->
    <PoangRad :vinnare="vinnare" :reset="reset" />
    <!--<div class="score">
      <p>
        <span id="spelare">{{ score.spelare }}</span> -
        <span id="dator">{{ score.dator }}</span>
      </p>
    </div> -->

    <!-- nollställ knapp -->

    <div class="score">
      <button id="nolla" @click="reset = true">Nollställ poängen</button>
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
