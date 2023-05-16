<!-- MapChart.vue -->
<template>
  <div class="chart-container">
    <div ref="chart" class="chart"></div>
  </div>
</template>

<script>
import echarts from 'echarts'

export default {
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  mounted () {
    this.chart = echarts.init(this.$refs.chart)
    this.renderChart(this.data)
  },
  beforeDestroy () {
    if (this.chart) {
      this.chart.dispose()
      this.chart = null
    }
  },
  methods: {
    renderChart (data) {
      // 渲染地图
    }
  }
}
</script>

<style scoped>
.chart-container {
  width: 100%;
  height: 0;
  padding-bottom: 60%;
  position: relative;
}

.chart {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
