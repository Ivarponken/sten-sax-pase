<script setup>
import { ref, watch } from 'vue'

const props = defineProps(['knappar', 'reset'])
const emit = defineEmits(['valdaKnappar'])

function spelarval(e) {
  let buttons = document.getElementsByClassName('alternativ')
  for (let b of buttons) {
    b.classList.remove('spelarval')
  }
  e.target.classList.add('spelarval')

  emit('valdaKnappar', { spelare: e.target.textContent, dator: datorval() })
}
function datorval() {
  let val = Math.floor(Math.random() * props.knappar.length)
  let buttons = document.getElementsByClassName('alternativ')
  for (let b of buttons) {
    b.classList.remove('datorval')
    b.title = ''
    if (b.textContent === props.knappar[val]) {
      b.classList.add('datorval')
      b.title = 'Datorns val'
    }
  }
  return props.knappar[val]
}
watch(
  () => props.reset,
  () => {
    if (props.reset) {
      let buttons = document.getElementsByClassName('alternativ')
      for (let b of buttons) {
        b.classList.remove('spelarval')
        b.classList.remove('datorval')
        b.title = ''
      }
    }
  },
)
</script>

<template>
  <div class="knapprad">
    <button v-for="knapp in props.knappar" class="alternativ" :key="knapp" @click="spelarval">
      {{ knapp }}
    </button>
  </div>
</template>
<style scoped>
button {
  padding: 0.6em 1.2em;
  font-size: 1.2em;
  background-color: cadetblue;
  border: 1px solid darkcyan;
  border-radius: 5px;
  cursor: pointer;
}
.knapprad {
  display: flex;
  justify-content: center;
  gap: 0.6em;
}
button.spelarval {
  background-color: #aaff00;
}
button.datorval {
  border: red solid 3px;
}
</style>
