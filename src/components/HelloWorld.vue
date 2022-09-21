<script setup lang="ts">
import { ref } from 'vue';
const canvas = ref<HTMLCanvasElement>();
let timeOutId = ref()

const draw = () => {
  if (!canvas.value) return
  const ctx: CanvasRenderingContext2D | null = canvas.value.getContext('2d')
  if (!ctx) return
  const image = ctx.createImageData(10, 10)
  // 青色にする
  const makeBlue = () => {
    for (let i = 0; i < image.data.length; i++) {
      image.data[i * 4] = 46
      image.data[i * 4 + 1] = 135
      image.data[i * 4 + 2] = 243
      image.data[i * 4 + 3] = 255
    }
  }
  const makeBrown = () => {
    for (let i = 0; i < image.data.length; i++) {
      image.data[i * 4] = 243
      image.data[i * 4 + 1] = 108
      image.data[i * 4 + 2] = 24
      image.data[i * 4 + 3] = 255
    }
  }

  let x = 0
  let y = 0

  timeOutId.value = setInterval(function drawImge() {
    makeBlue()
    ctx.putImageData(image, x, y * 10)
    y++

  }, 1000)
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

