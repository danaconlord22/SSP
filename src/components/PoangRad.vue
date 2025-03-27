<script setup>
import { ref, watch } from 'vue'

const props = defineProps(['vinnare', 'reset'])
const score = ref({ spelare: 0, dator: 0 })

watch(props, () => {
  if (props.vinnare === 'spelare') {
    score.value.spelare++
  } else if (props.vinnare === 'dator') {
    score.value.dator++
  }
})

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
      <span id="spelare" class="player-score">{{ score.spelare }}</span>
      <span class="separator">:</span>
      <span id="dator" class="computer-score">{{ score.dator }}</span>
    </p>
  </div>
</template>

<style scoped>
.score {
  font-size: 2.5em;
  text-align: center;
  margin: 1em 0;
  text-shadow: 0 0 10px #4d4dff;
}

.player-score,
.computer-score {
  display: inline-block;
  min-width: 1.5em;
  padding: 0.2em;
  color: #4d4dff;
}

.separator {
  color: #8a2be2;
  margin: 0 0.5em;
  animation: blink 1s infinite;
}

@keyframes blink {
  50% {
    opacity: 0;
  }
}
</style>
