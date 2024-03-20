<template>
  <div class="calculatrice">
    <div id="result" class="screen">{{ screen }}</div>
    <div class="calculatrice-keys">
      <button v-for="button in buttons" :key="button" @click="onButtonClick">
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

function onButtonClick(event) {
  const last_click = event.target.innerText
  if (last_click === 'C') {
    screen.value = ''
    flag = 0
  } else if (last_click === '=') {
    flag = 1
    screen.value = math.evaluate(screen.value).toString()
    console.log('Évaluation de:', screen.value)
    console.log(flag)
  } else {
    if (last_click === '+' || last_click === '-' || last_click === '*' || last_click === '/') {
      screen.value += last_click
      flag = 0
    } else {
      console.log(flag)
      if (flag === 1) {
        screen.value = ''
        screen.value += last_click
      } else {
        flag = 0
        screen.value += last_click
      }
    }
  }
}
</script>
