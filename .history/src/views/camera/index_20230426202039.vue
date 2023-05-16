<template>
  <div class="container">
    <div class="sidebar">
      <div class="sidebar-header">{{ station }}</div>
      <div class="toolbar">
        <el-button-group>
          <!-- <el-button v-for="pole in poles" :key="pole" @click="currentPole = pole">{{ pole }}</el-button> -->
          <el-button
            v-for="pole in poles"
            :key="pole"
            @click="handleChangePole(pole)"
            >{{ pole }}</el-button
          >
        </el-button-group>
      </div>
    </div>
    <div class="main">
      <div class="header">
        <el-button-group>
          <el-button
            v-for="part in parts"
            :key="part"
            @click="currentPart = part"
            >{{ part }}</el-button
          >
        </el-button-group>
        <el-button-group>
          <el-button
            v-for="image in images[currentPoleIndex]"
            :key="image"
            @click="currentImage = image"
            >{{ image }}</el-button
          >
        </el-button-group>
        <div class="buttonBox">
          <router-link to="/home">
            <el-tooltip content="退出" placement="top">
              <el-button
                type="primary"
                icon="el-icon-s-home"
                circle
              ></el-button>
            </el-tooltip>
          </router-link>
        </div>
      </div>
      <div class="canvas-container">
        <canvas
          ref="myCanvas"
          :width="canvasWidth"
          :height="canvasHeight"
        ></canvas>
      </div>
      <div class="footer">当前选择：{{ currentPole }} - {{ currentPart }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      station: '站台名称',
      poles: [
        '杆号01',
        '杆号02',
        '杆号03',
        '杆号04',
        '杆号05',
        '杆号06',
        '杆号07',
        '杆号08',
        '杆号09',
        '杆号10',
        '杆号11',
        '杆号12',
        '杆号13',
        '杆号14'
      ],
      parts: [
        '部位1',
        '部位2',
        '部位3',
        '部位4',
        '部位5',
        '部位6',
        '部位7',
        '部位8',
        '部位9',
        '部位10'
      ],
      images: {
        部位1: require('@/assets/images/head.png'),
        部位2: require('@/assets/images/lbx.png'),
        部位3: require('@/assets/images/logo.png'),
        部位4: require('@/assets/images/map.png')
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
      // Clear the canvas before drawing a new image
      ctx.clearRect(0, 0, canvas.width, canvas.height)
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
      const imageUrl = this.images[this.currentPart]
      // provide the image url to the img element
      img.src = imageUrl
    },
    handleChangePole (pole) {
      this.currentPole = pole
      const index = (this.poles.indexOf(pole) + 1) % 4
      this.currentPart = `部位${index + 1}`
      this.drawCanvas()
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
