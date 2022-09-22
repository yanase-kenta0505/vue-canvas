<script setup lang="ts">
import { ref } from 'vue';
const canvas = ref<HTMLCanvasElement>();
let timeOutId = ref()

let x = ref(0)
let y = ref(0)
let keyNum = ref(170)

let randomNum = ref(Math.floor(Math.random() * 150 + 150))


const draw = () => {
  if (!canvas.value) return
  const ctx: CanvasRenderingContext2D | null = canvas.value.getContext('2d')
  if (!ctx) return
  const image = ctx.createImageData(5, 5)
  // 青色にする
  const makeBlue = () => {
    for (let i = 0; i < image.data.length; i++) {
      image.data[i * 4] = 46
      image.data[i * 4 + 1] = 135
      image.data[i * 4 + 2] = 243
      image.data[i * 4 + 3] = 255
    }
  }
  // 赤色にする
  const makeRed = () => {
    for (let i = 0; i < image.data.length; i++) {
      image.data[i * 4] = 243
      image.data[i * 4 + 1] = 45
      image.data[i * 4 + 2] = 53
      image.data[i * 4 + 3] = 255
    }
  }

  // 茶色にする
  const makeYellow = () => {
    for (let i = 0; i < image.data.length; i++) {
      image.data[i * 4] = 299
      image.data[i * 4 + 1] = 243
      image.data[i * 4 + 2] = 73
      image.data[i * 4 + 3] = 255
    }
  }

  // 緑色にする
  const makeGreen = () => {
    for (let i = 0; i < image.data.length; i++) {
      image.data[i * 4] = 207
      image.data[i * 4 + 1] = 243
      image.data[i * 4 + 2] = 0
      image.data[i * 4 + 3] = 255
    }
  }

  makeBlue()

  const test = () => {
    ctx.putImageData(image, x.value, y.value * 5)
    y.value++
    if (!canvas.value) return

    let num = y.value * 5
    console.log(num)
    if (150 < num && num < 170) {
      makeRed()
    } else if (keyNum.value < num && num < keyNum.value + 15) {
      makeGreen()
    } else if (keyNum.value + 15 < num && num < keyNum.value + 30) {
      makeYellow()
    } else if (keyNum.value + 30 < num && num < keyNum.value + 60) {
      makeBlue()
    } else if (num > 300) {
      y.value = 0
      x.value += 5
      keyNum.value += 3
    }
  }

  timeOutId.value = setInterval(test, 1)
}

const stop = () => clearInterval(timeOutId.value)

</script>
<template>
  <h1>canvas lesson</h1>
  <canvas width="300" height="300" ref='canvas' />
  <button @click="draw">draw</button>
  <button @click="stop">stop</button>

</template>
  
<style scoped>
canvas {
  border: 3px solid red;
}
</style>
  
  