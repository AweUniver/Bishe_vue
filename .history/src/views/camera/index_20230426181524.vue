<template>
  <div class="container">
    <div class="sidebar">
      <div class="sidebar-header">{{ station }}</div>
      <div class="toolbar">
        <el-button-group>
          <el-button v-for="pole in poles" :key="pole" @click="changeImage(pole, currentPart)">{{ pole }}</el-button>
        </el-button-group>
      </div>
    </div>
    <div class="main">
      <div class="header">
        <el-button-group>
          <el-button v-for="part in parts" :key="part" @click="changeImage(currentPole, part)">{{ part }}</el-button>
        </el-button-group>
      </div>
      <div class="canvas-container">
        <canvas ref="myCanvas" :width="canvasWidth" :height="canvasHeight"></canvas>
      </div>
      <div class="footer">
        当前选择：{{ currentPole }} - {{ currentPart }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      station: '站台名称',
      poles: ['杆号1', '杆号2', '杆号3', '杆号4'],
      parts: ['部位1', '部位2', '部位3', '部位4'],
      images: {
        '杆号1': {
          '部位1': 'url/to/pole1-part1/image',
          '部位2': 'url/to/pole1-part2/image',
          '部位3': 'url/to/pole1-part3/image',
          '部位4': 'url/to/pole1-part4/image',
        },
        '杆号2': {
          '部位1': 'url/to/pole2-part1/image',
          '部位2': 'url/to/pole2-part2/image',
          '部位3': 'url/to/pole2-part3/image',
          '部位4': 'url/to/pole2-part4/image',
        },
        '杆号3': {
          '部位1': 'url/to/pole3-part1/image',
          '部位2': 'url/to/pole3-part2/image',
          '部位3': 'url/to/pole3-part3/image',
          '部位4': 'url/to/pole3-part4/image',
        },
        '杆号4': {
          '部位1': 'url/to/pole4-part1/image',
          '部位2': 'url/to/pole4-part2/image',
          '部位3': 'url/to/pole4-part3/image',
          '部位4': 'url/to/pole4-part4/image',
        },
      },
      currentPart: '部位1',
      currentPole: '杆号1',
      canvasWidth: 1041,
      canvasHeight: 600
    };
  },
  mounted() {
    this.drawCanvas();
  },
  methods: {
    changeImage(pole, part) {
      this.currentPole = pole;
      this.currentPart = part;
      this.drawCanvas();
    },
