<template>
  <div ref="chart" style="width: 100%; height: 600px;"></div>
</template>

<script>
import echarts from 'echarts'

export default {
  mounted () {
    const chart = echarts.init(this.$refs.chart)
    chart.setOption({
      series: [
        {
          name: '中国',
          type: 'map',
          mapType: 'china',
          label: {
            show: true
          },
          roam: false,
          data: []
        }
      ]
    })
  }
}
</script>

<style>
/* 可以在这里添加样式 */
</style>
