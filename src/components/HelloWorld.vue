<script setup lang="ts">
import { ref } from 'vue';
const canvas = ref<HTMLCanvasElement>();
let timeOutId = ref()

let x = ref(0)
let y = ref(0)


const draw = () => {
  if (!canvas.value) return
  const ctx: CanvasRenderingContext2D | null = canvas.value.getContext('2d')
  if (!ctx) return
  const image = ctx.createImageData(10, 10)
  // 青色にする

  for (let i = 0; i < image.data.length; i++) {

    image.data[i * 4] = 46
    image.data[i * 4 + 1] = 135
    image.data[i * 4 + 2] = 243
    image.data[i * 4 + 3] = 255
  }

  const makeBrown = () => {
    for (let i = 0; i < image.data.length; i++) {
      console.log('yaa')
      image.data[i * 4] = 243
      image.data[i * 4 + 1] = 108
      image.data[i * 4 + 2] = 24
      image.data[i * 4 + 3] = 255
    }
  }

  timeOutId.value = setInterval(function test() {
    ctx.putImageData(image, x.value, y.value * 10)
    y.value++
    if (!canvas.value) return
    if (y.value * 10 === canvas.value.height || y.value * 10 === 0) {
      // 青色に変更
      for (let i = 0; i < image.data.length; i++) {
        image.data[i * 4] = 46
        image.data[i * 4 + 1] = 135
        image.data[i * 4 + 2] = 243
        image.data[i * 4 + 3] = 255
      }
      y.value = 0
      x.value += 10
    } else if (y.value * 10 === canvas.value.height / 2) {
      // 茶色に変更
      for (let i = 0; i < image.data.length; i++) {
        image.data[i * 4] = 243
        image.data[i * 4 + 1] = 108
        image.data[i * 4 + 2] = 24
        image.data[i * 4 + 3] = 255
      }
    }
  }, 10)
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

