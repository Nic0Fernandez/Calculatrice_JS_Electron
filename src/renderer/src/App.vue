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
var flag = 0

function onButtonClick(button) {
  if (button === 'C') {
    screen.value = ''
    flag = 0
  } else if (button === '=') {
    flag = 1
    screen.value = math.evaluate(screen.value).toString()
    console.log('Évaluation de:', screen.value)
    console.log(flag)
  } else {
    if (button === '+' || button === '-' || button === '*' || button === '/') {
      screen.value += button
      flag = 0
    } else {
      console.log(flag)
      if (flag === 1) {
        screen.value = ''
        screen.value += button
      } else {
        flag = 0
        screen.value += button
      }
    }
  }
}

</script>
