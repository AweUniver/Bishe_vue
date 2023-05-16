<template>
  <div class="container">
    <div class="chart">
      <chart :options="chartOptions" :updateOptions="updateOptions" />
    </div>
  </div>
</template>

<script>
import Chart from 'echarts'
import axios from 'axios'

export default {
  name: 'HomePage',
  components: {
    Chart
  },
  data () {
    return {
      chartOptions: null
    }
  },
  mounted () {
    this.getChartData()
  },
  methods: {
    getChartData () {
      axios.get('/api/data').then((response) => {
        this.chartOptions = response.data
      })
    },
    updateOptions (newOptions) {
      this.chartOptions = newOptions
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.chart {
  width: 80%;
  height: 80%;
}
</style>
