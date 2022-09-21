<script setup lang="ts">
import { ref } from 'vue';
const canvas = ref<HTMLCanvasElement>();
let timeOutId = ref()

let x = ref(0)
let y = ref(0)
let randomNum = ref(Math.floor(Math.random() * 150 + 150))


const draw = () => {
  if (!canvas.value) return
  const ctx: CanvasRenderingContext2D | null = canvas.value.getContext('2d')
  if (!ctx) return
  const image = ctx.createImageData(4, 300)
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
  const makeBrown = () => {
    for (let i = 0; i < image.data.length; i++) {
      image.data[i * 4] = 243
      image.data[i * 4 + 1] = 160
      image.data[i * 4 + 2] = 0
      image.data[i * 4 + 3] = 255
    }
  }

  makeBlue()

  const test = () => {
    ctx.putImageData(image, x.value, 0)
    x.value += 5
  }

  timeOutId.value = setInterval(test, 10)

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
  
  