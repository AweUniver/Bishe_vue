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
        部位1: 'url/to/part1/image',
        部位2: 'url/to/part2/image',
        部位3: 'url/to/part3/image',
        部位4: 'url/to/part4/image'
      },
      currentPart: '部位1',
      currentPole: '杆号1',
      canvasWidth: 1041,
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
        const canvasAspectRatio = canvas.width / canvas.height
        const imageAspectRatio = img.width / img.height
        let drawWidth = canvas.width
        let drawHeight = canvas.height
        if (canvasAspectRatio > imageAspectRatio) {
          drawHeight = canvas.width / imageAspectRatio
        } else {
          drawWidth = canvas.height * imageAspectRatio
        }
        ctx.drawImage(img, 0, 0, drawWidth, drawHeight)
      }
      // provide mock data for the image url
      // img.src = 'https://via.placeholder.com/800x600'
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
  flex: 0 0 150px;
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
  flex: 1;
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
