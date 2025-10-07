<script setup>
import { ref } from 'vue'
import KnappRad from './components/knapprad.vue'
import ResultatRad from './components/ResultatRad.vue'
import PoangRad from './components/PoangRad.vue'

const knappar = ref(['Sten', 'Sax', 'Påse', 'Lizard', 'Spock'])
const score = ref({ spelare: 0, dator: 0 })
const resultat = ref('Du vann!')
const vinnare = ref('')
const reset = ref(true)

function hittaVinnare(valdaKnappar) {
  reset.value = false
  vinnare.value = ''
  let spelare = knappar.value.indexOf(valdaKnappar.spelare)
  let dator = knappar.value.indexOf(valdaKnappar.dator)
  resultat.value = { spelare: spelare, dator: dator }
}

function raknaPoang(v) {
  if (v === 'spelare') {
    score.value.spelare++
  } else {
    score.value.dator++
  }
  vinnare.value = v
}
</script>

<template>
  <header>
    <h1>Sten, sax, påse!</h1>
  </header>

  <main>
    <KnappRad :knappar="knappar" :reset="reset" @valda-knappar="hittaVinnare" />
    <ResultatRad :valda-knappar="resultat" :reset="reset" @vinnare="raknaPoang" />
    <PoangRad :vinnare="vinnare" :reset="reset" />
    <button id="nolla" @click="reset = true">Nollställ Poäng</button>
  </main>
</template>

<style scoped>
header {
  text-align: center;
  margin-bottom: 1.2em;
}
#nolla {
  margin: auto;
  display: block;
  color: white;
  margin-top: 2em;
  padding: 1em 2em;
  font-size: 0.8em;
  background-color: darkred;
  border: none;
  border-radius: 5px;
}
#nolla:hover {
  background-color: red;
  cursor: pointer;
}
</style>
