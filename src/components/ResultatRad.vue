<script setup>
import { ref, watch } from 'vue'

const props = defineProps(['valdaKnappar', 'reset'])
const emit = defineEmits(['vinnare'])

const resultat = ref('Låt spelet börja!')

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
    // Olika paritet - Lägre talet vinner
    if (props.valdaKnappar.spelare < props.valdaKnappar.dator) {
      resultat.value = 'Du vann!'
      emit('vinnare', 'spelare')
    } else {
      resultat.value = 'Datorn vann!'
      emit('vinnare', 'dator')
    }
  }
})

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
  margin: 1.5em 0;
  padding: 1em;
  border: 2px solid #4d4dff;
  background-color: rgba(77, 77, 255, 0.1);
  text-shadow: 0 0 5px #4d4dff;
  animation: fadeIn 0.5s ease-in;
  box-shadow: inset 0 0 20px rgba(138, 43, 226, 0.2);
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
