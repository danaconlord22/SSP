<script setup>
// Importera nödvändiga Vue-funktioner
import { ref, watch } from 'vue'

// Ta emot props från förälderkomponenten
const props = defineProps(['vinnare', 'reset'])

// Håll reda på poängställningen
const score = ref({ spelare: 0, dator: 0 })

// Övervaka ändringar i props för att uppdatera poängen
watch(props, () => {
  if (props.vinnare === 'spelare') {
    score.value.spelare++
  } else if (props.vinnare === 'dator') {
    score.value.dator++
  }
})

// Övervaka reset-prop för att nollställa poängen
watch(
  () => props.reset,
  () => {
    if (props.reset) {
      score.value.spelare = 0
      score.value.dator = 0
    }
  }
)
</script>

<template>
  <div class="score">
    <p>
      <span id="spelare">
        {{ score.spelare }}
      </span>
      -
      <span id="dator">
        {{ score.dator }}
      </span>
    </p>
  </div>
</template>

<style scoped></style>
