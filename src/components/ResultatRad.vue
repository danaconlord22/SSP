<script setup>
// Importera nödvändiga Vue-funktioner
import { ref, watch } from 'vue'

// Ta emot props och skapa emit
const props = defineProps(['valdaKnappar', 'reset'])
const emit = defineEmits(['vinnare'])

// Håll reda på spelresultatet
const resultat = ref('Låt spelet börja!')

// Övervaka props för att avgöra vinnare baserat på paritet
watch(props, () => {
  console.log('Resultatet har ändrats till:', props.valdaKnappar)
  if (props.valdaKnappar.spelare == props.valdaKnappar.dator) {
    resultat.value = 'Oavgjort!'
  } else if (props.valdaKnappar.spelare % 2 == props.valdaKnappar.dator % 2) {
    // Samma paritet - Högsta talet vinner
    if (props.valdaKnappar.spelare > props.valdaKnappar.dator) {
      resultat.value = 'Du vann!'
      emit('vinnare', 'spelare')
    } else {
      resultat.value = 'Datorn vann!'
      emit('vinnare', 'dator')
    }
  } else {
    // Olika paritet - Lägsta talet vinner
    if (props.valdaKnappar.spelare < props.valdaKnappar.dator) {
      resultat.value = 'Du vann!'
      emit('vinnare', 'spelare')
    } else {
      resultat.value = 'Datorn vann!'
      emit('vinnare', 'dator')
    }
  }
})

// Övervaka reset-prop för att återställa resultatmeddelandet
watch(
  () => props.reset,
  () => {
    if (props.reset) {
      resultat.value = 'Spelet har börjat'
    }
  }
)
</script>

<template>
  <div class="resultat">
    <p id="resultat">{{ resultat }}</p>
  </div>
</template>

<style scoped>
.resultat {
  font-size: 1.2em;
  text-align: center;
  margin: 1.2em 0;
}
</style>
