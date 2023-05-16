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
  data () {
    return {
      station: '站台名称',
      poles: ['杆号1', '杆号2', '杆号3', '杆号4'],
      parts: ['部位1', '部位2', '部位3', '部位4'],
      images: {
        杆号1: {
          部位1: 'url/to/pole1/part1/image',
          部位2: 'url/to/pole1/part2/image',
          部位3: 'url/to/pole1/part3/image',
          部位4: 'url/to/pole1/part4/image'
        },
        杆号2: {
          部位1: 'url/to/pole2/part1/image',
          部位2: 'url/to/pole2/part2/image',
          部位3: 'url/to/pole2/part3/image',
          部位4: 'url/to/pole2/part4/image'
        },
        杆号3: {
          部位1: 'url/to/pole3/part1/image',
          部位2: 'url/to/pole3/part2/image',
          部位3: 'url/to/pole3/part3/image',
          部位4: 'url/to/pole3/part4/image'
        },
        杆号4: {
          部位1: 'url/to/pole4/part1/image',
          部位2: 'url/to/pole4/part2/image',
          部位3: 'url/to/pole4/part3/image',
          部位4: 'url/to/pole4/part4/image'
        }
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
    },
    currentImage () {
      return this.images[this.currentPole][this.currentPart]
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
        ctx.clearRect(0, 0, canvas.width, canvas.height) // 清空画布
        ctx.drawImage(img, 0, 0, drawWidth, drawHeight)
      }
      // provide mock data for the image url
      img.src = this.currentImage
    },
    changePole (pole) {
      this.currentPole = pole
      this.currentPart = '部位1' // 切换杆号时，部位默认为第一个
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
