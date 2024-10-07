<script setup>

import { ref } from 'vue';

const score = ref({spelare: 0, dator: 0});
const resultat = ref("Du vann!");

</script>

<template>
  <!-- rubrik -->
  <header>
    <h1>Sten, Sax, Påse!</h1>
  </header>

  <!-- knapparna -->
  <main>
    <div class="knapprad">
      <button>Sten</button>
      <button>Sax</button>
      <button>Påse</button>
    </div>

    <!-- resultat -->
    <div class="resultat">
      <p id="resultat">{{resultat}}</p>
    </div>

    <!-- poäng -->
    <div class="score">
      <p>
        <span id="spelare">{{score.spelare}}</span> - 
        <span id="dator">{{score.dator}}</span>
      </p>

    </div>
  </main>
</template>

<style scoped>

header {
    text-align: center;
    margin-bottom: 1.2em;
}

button {
    padding: .6em 1.2em;
    font-size: 1.2em;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    border-radius: 5px;
    cursor: pointer;
}

.knapprad {
    display: flex;
    justify-content: center;
    gap: .6em;
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

</style>
