<template>
  <div class="home-page">
    <div class="map-container" ref="map"></div>
  </div>
</template>

<script>
import echarts from 'echarts'

export default {
  mounted () {
    // 初始化echarts
    this.map = echarts.init(this.$refs.map)
    this.renderMap()
  },
  methods: {
    async renderMap () {
      // 获取地图数据，此处为示例，实际使用时应从API获取数据
      const response = await axios.get('/api/mapData')
      const mapData = response.data

      // echarts配置
      const option = {
        title: {
          text: '中国地图',
          left: 'center',
          top: 20
        },
        tooltip: {
          trigger: 'item'
        },
        visualMap: {
          min: 0,
          max: 1000,
          left: 'left',
          top: 'bottom',
          text: ['高', '低'],
          calculable: true
        },
        series: [{
          name: '地图数据',
          type: 'map',
          mapType: 'china',
          roam: false,
          label: {
            show: true
          },
          data: mapData
        }]
      }

      // 使用配置渲染echarts地图
      this.map.setOption(option)
    }
  }
}
</script>

<style>
.map-container {
  height: 600px;
}
</style>
