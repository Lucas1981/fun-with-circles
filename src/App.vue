<template>
  <div id="app">
    <div class="container">
      <h1 class="text-center">Fun With Circles</h1>
      <div class="wrapper">
        <canvas class="canvas" ref="canvas"></canvas>
        <div class="card controls">
          <div class="card-body">
            <my-input
              v-model="turns"
              label="Turns"
              type="number"
              @input="drawPolygon"
            />
            <my-input
              v-model="radius"
              label="Radius"
              type="number"
              @input="drawPolygon"
            />
            <my-input
              v-model="skip"
              label="Skip"
              type="number"
              @input="drawPolygon"
            />
            <my-input
              v-model="thickness"
              label="Thickness"
              type="number"
              @input="drawPolygon"
            />
            <my-input
              v-model="fillColor"
              label="Fill color"
              type="color"
              @input="drawPolygon"
            />
            <my-input
              v-model="strokeColor"
              label="Stroke color"
              type="color"
              @input="drawPolygon"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MyInput from './components/my-input.vue';

const width = 800;
const height = 512;
const radius = 200;
const degreesToRadians = degrees => degrees * Math.PI / 180;
const fillColor = '#000000';
const strokeColor = '#008800';

export default {
  name: 'app',
  data: () => ({
    canvas: null,
    ctx: null,
    turns: 11,
    skip: 1,
    thickness: 3,
    radius,
    width,
    height,
    fillColor,
    strokeColor
  }),
  components: {
    MyInput
  },
  computed: {
    centerX() { return this.width / 2; },
    centerY() { return this.height / 2; },
    turn() { return 360 / this.turns; }
  },
  mounted() {
    this.canvas = this.$refs.canvas;
    this.ctx = this.canvas.getContext('2d');
    this.canvas.width = this.width;
    this.canvas.height = this.height;
    this.drawPolygon();
  },
  methods: {
    drawPolygon() {
      this.ctx.clearRect(0, 0, this.width, this.height);
      this.ctx.strokeStyle = this.strokeColor;
      this.ctx.fillStyle = this.fillColor;
      this.ctx.lineWidth = this.thickness;
      this.ctx.beginPath();
      for (let i = 0; i < this.turns; i++) {
        const x = Math.sin(degreesToRadians(this.turn * (i * this.skip))) * this.radius;
        const y = Math.cos(degreesToRadians(this.turn * (i * this.skip))) * this.radius;
        if (i === 0) this.ctx.moveTo(this.centerX + x, this.centerY + y);
        else this.ctx.lineTo(this.centerX + x, this.centerY + y);
      }
      this.ctx.closePath();
      this.ctx.fill();
      this.ctx.stroke();
    }
  }
}
</script>

<style>
.wrapper {
  display: flex;
  justify-content: center;
  padding-top: 16px;
  padding-bottom: 16px;
}

.canvas {
  background-color: black;
  width: 800px;
}

.controls {
  margin-left: 8px;
  width: 256px;
}
</style>
