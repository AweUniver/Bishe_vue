<template>
  <div class="page-container">
    <div class="sidebar-container">
      <div class="site-container">
        <div class="site-title">站点</div>
        <div v-for="(site, index) in siteList" :key="index" class="site-item">{{ site }}</div>
      </div>
      <div class="button-container">
        <div class="button-title">杆号</div>
        <div v-for="(button, index) in buttonList" :key="index" class="button-item">{{ button }}</div>
      </div>
    </div>
    <div class="canvas-container">
      <div class="button-menu">
        <div class="button-title">高铁部位</div>
        <div v-for="(button, index) in buttonMenu" :key="index" class="button-item">{{ button }}</div>
      </div>
      <canvas ref="mainCanvas"></canvas>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data () {
    return {
      siteList: [
        '站点1',
        '站点2',
        '站点3',
        '站点4',
        '站点5'
      ],
      buttonList: [
        '杆号1',
        '杆号2',
        '杆号3',
        '杆号4',
        '杆号5'
      ],
      buttonMenu: [
        '头部',
        '车厢1',
        '车厢2',
        '车厢3',
        '尾部'
      ]
    }
  },
  computed: {
    ...mapState({
      canvasData: state => state.canvasData
    })
  },
  mounted () {
    const canvas = this.$refs.mainCanvas
    const ctx = canvas.getContext('2d')
    ctx.fillStyle = '#f2f2f2'
    ctx.fillRect(0, 0, canvas.width, canvas.height)

    // 渲染图片
    const img = new Image()
    img.src = this.canvasData.imgUrl
    img.onload = () => {
      ctx.drawImage(img, 0, 0, canvas.width, canvas.height)
    }
  }
}
</script>

<style scoped>
  .page-container {
    display: flex;
    height: 100%;
  }
  .sidebar-container {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: #fff;
  }
  .site-container, .button-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }
  .site-title, .button-title {
    font-weight: bold;
    font-size: 16px;
    margin-bottom: 10px;
  }
  .site-item, .button-item {
    font-size: 14px;
    line-height: 24px;
    color: rgba(0, 0, 0, .65);
    cursor: pointer;
  }
  .button-item:hover {
    color: #1890ff;
  }
  .canvas-container {
    flex: 3;
    display: flex;
    flex-direction: column;
    background-color: #f2f2f2;
    padding: 20px;
  }
  .button-menu {
    display: flex;
    margin-bottom: 20px;
  }
  .canvas-container .button-title {
    font-weight: bold;
    font-size: 18px;
    margin-right: 50px;
    margin-bottom: 10px;
  }
  .button-item {
    font-size: 14px;
    line-height: 1.5;
    padding: 8px 16px;
    margin-right: 10px;
    margin-bottom: 10px;
    color: #666;
    background-color: #f2f2f2;
    border-radius: 4px;
    cursor: pointer;
  }
  .button-item:hover {
    color: #fff;
    background-color: #1890ff;
  }
</style>
