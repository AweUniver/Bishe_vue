<template>
  <div class="container">
    <div class="sidebar">
      <div class="sidebar-header">{{ station }}</div>
      <div class="toolbar">
        <el-button-group>
          <el-button v-for="pole in poles" :key="pole" @click="currentPole = pole">{{ pole }}</el-button>
        </el-button-group>
      </div>
    </div>
    <div class="main">
      <div class="header">
        <el-button-group>
          <el-button v-for="part in parts" :key="part" @click="currentPart = part">{{ part }}</el-button>
        </el-button-group>
      </div>
      <div class="canvas-container">
        <canvas ref="myCanvas" :width="canvasWidth" :height="canvasHeight"></canvas>
        <div class="pole-numbers">
          <div v-for="(pole, index) in poles" :key="index" class="pole-number">{{ pole }}</div>
        </div>
      </div>
      <div class="footer">
        当前选择：{{ currentPole }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      station: '站台名称',
      poles: ['杆号1', '杆号2', '杆号3', '杆号4'],
      parts: ['部位1', '部位2', '部位3', '部位4'],
      images: {
  高架桥: 'https://via.placeholder.com/800x600.png?text=%E9%AB%98%E6%9E%B6%E6%A1%A5',
  隧道口: 'https://via.placeholder.com/800x600.png?text=%E9%9A%A7%E9%81%93%E5%8F%A3',
  车站: 'https://via.placeholder.com/800x600.png?text=%E8%BD%A6%E7%AB%99',
  道岔: 'https://via.placeholder.com/800x600.png?text=%E9%81%93%E5%B2%94',
  轨道: 'https://via.placeholder.com/800x600.png?text=%E8%BD%A8%E9%81%93'
},
,
      currentPart: '部位1',
      currentPole: '杆号1',
      canvasWidth: 800,
      canvasHeight: 600
    }
  },
  mounted () {
    this.drawCanvas()
  },
  computed: {
    currentPoleIndex () {
      return this.poles.indexOf(this.currentPole)
    }
  },
  methods: {
    drawCanvas () {
      const canvas = this.$refs.myCanvas
      const ctx = canvas.getContext('2d')
      const img = new Image()
      img.onload = function () {
        ctx.drawImage(img, 0, 0, canvas.width, canvas.height)
      }
      // provide mock data for the image url
      img.src = 'https://via.placeholder.com/800x600'
    }
  },
  watch: {
    currentPart () {
      this.drawCanvas()
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  height: 100vh;
}

.sidebar {
  flex: 1;
  display: flex;
  flex-direction: column;
  border-right: 1px solid #dcdfe6;
  padding: 20px;
}

.sidebar-header {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 20px;
}

.toolbar {
  margin-bottom: 20px;
}

.main {
  flex: 3;
  display: flex;
  flex-direction: column;
}

.header {
  height: 80px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 1px solid #dcdfe6;
}

.canvas-container {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.el-button-group {
  margin-right: 10px;
}

.el-button--primary {
  background-color: #409eff;
  border-color: #409eff;
}

.el-button--primary:focus,
.el-button--primary:hover {
  background-color: #66b1ff;
  border-color: #66b1ff;
}

.el-tabs__item {
  height: 40px;
  line-height: 40px;
  padding: 0 20px;
  margin-right: 10px;
}

canvas {
  max-width: 100%;
  max-height: 100%;
}
</style>
