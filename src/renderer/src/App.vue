<template>
  <div class="calculatrice">
    <div class="screen">{{ screen }}</div>
    <div class="calculatrice-keys">
      <button v-for="button in buttons" :key="button" @click="onButtonClick(button)">
        {{ button }}
      </button>
    </div>
  </div>
</template>

<script setup>
import * as math from 'mathjs'
import { reactive, ref } from 'vue'

const screen = ref('')
const buttons = [1, 2, 3, '+', 4, 5, 6, '-', 7, 8, 9, '*', 0, 'C', '=', '/']

function onButtonClick(button) {
  var flag = 0
  if (button === 'C') {
    screen.value = ''
  } else if (button === '=') {
    flag = 1
    screen.value = math.evaluate(screen.value).toString()
    console.log('Évaluation de:', screen.value)
  } else {
    if (flag === 1) {
      if (button === '+' || button === '-' || button === '*' || button === '/'){
        screen.value += button
      } else {
        screen.value = ''
        screen.value += button
      }
    }
  }
}
</script>
