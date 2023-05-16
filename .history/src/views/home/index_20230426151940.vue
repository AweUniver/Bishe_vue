<template>
  <div class="home">
    <div class="map-container">
      <div ref="map" class="map"></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import * as echarts from 'echarts'
import Mock from 'mockjs'

Mock.mock('/api/data', 'get', {
  'data|34': [{
    name: '@province',
    'value|1-100': 50
  }]
})

export default {
  name: 'Home',
  data () {
    return {
      mapChart: null
    }
  },
  mounted () {
    this.mapChart = echarts.init(this.$refs.map)
    axios.get('/api/data')
      .then(response => {
        this.renderMap(response.data.data)
      })
      .catch(error => {
        console.log(error)
      })
  },
  methods: {
    renderMap (data) {
      echarts.registerMap('china', require('@/assets/china.json'))
      this.mapChart.setOption({
        tooltip: {
          trigger: 'item',
          formatter: '{b}<br/>{c}'
        },
        visualMap: {
          min: 0,
          max: 100,
          left: 'left',
          top: 'bottom',
          text: ['高', '低'],
          calculable: true,
          color: ['#2d7df6', '#2b9ff5', '#3ac3ff', '#4be1ff', '#92f0ff']
        },
        series: [{
          name: '数据名称',
          type: 'map',
          mapType: 'china',
          label: {
            show: true,
            color: 'rgba(0,0,0,0.4)'
          },
          data: data
        }]
      })
    }
  }
}
</script>

<style scoped>
.map-container {
  width: 100%;
  height: 100%;
}

.map {
  width: 100%;
  height: 100%;
}
</style>
