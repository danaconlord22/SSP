<script setup>
import { ref } from 'vue'

import KnappRad from './components/KnappRad.vue'
import ResultatRad from './components/ResultatRad.vue'
import PoangRad from './components/PoangRad.vue'

const knappar = ref([
  'Warrior',
  'Mage',
  'Rogue',
  'Paladin',
  'Warlock',
  'Priest',
  'Hunter',
  'Druid',
  'Shaman'
])
const resultat = ref({})
const vinnare = ref('')
const reset = ref(true)

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
  <div class="game-container">
    <header>
      <h1>Sten, Sax, Påse++</h1>
    </header>

    <main>
      <KnappRad :knappar="knappar" @valda-knappar="hittaVinnare" :reset="reset" />
      <ResultatRad :valda-knappar="resultat" @vinnare="raknaPoang" :reset="reset" />
      <PoangRad :vinnare="vinnare" :reset="reset" />

      <div class="reset-container">
        <button id="nolla" @click="reset = true">Nollställ poängen</button>
      </div>
    </main>
  </div>
</template>

<style scoped>
.game-container {
  padding: 2em;
}

header {
  margin-bottom: 2em;
}

.reset-container {
  text-align: center;
  margin-top: 2em;
}

#nolla {
  padding: 0.5em 1em;
  font-size: 0.8em;
  background-color: #0a0014;
  border: 2px solid #8a2be2;
  color: #8a2be2;
  cursor: pointer;
  font-family: 'Press Start 2P', cursive;
  text-transform: uppercase;
  transition: all 0.2s ease;
  box-shadow: 0 0 10px #8a2be2;
}

#nolla:hover {
  background-color: #8a2be2;
  color: #0a0014;
  transform: scale(1.05);
  box-shadow:
    0 0 15px #8a2be2,
    0 0 30px #4d4dff;
}
</style>
