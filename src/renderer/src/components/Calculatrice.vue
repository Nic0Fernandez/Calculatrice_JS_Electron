
<template>
  <div class="calculatrice">
    <div class="screen">{{ screen }}</div>
    <div class="calculatrice_keys">
      <button v-for="button in buttons" :key="button" @click="onButtonClick(button)">
        {{ button }}
      </button>
    </div>
  </div>
</template>

<script setup>
import * as math from 'mathjs'
import { reactive, ref } from 'vue'

const screen = ref('');
const buttons = [1, 2, 3, '+', 4, 5, 6, '-', 7, 8, 9, '*', 0, 'C', '=', '/']

function onButtonClick(button) {
  if (button === 'C') {
    screen.value = ''
  } else if (button === '=') {
    screen.value = math.evaluate(screen.value).toString()
    console.log('Évaluation de:', screen.value)
  } else {
    screen.value += button
  }
}
</script>
