<!-- Home.vue -->
<template>
  <div class="home">
    <h1>全国数据分布</h1>
    <map-chart :data="mapData" />
  </div>
</template>

<script>
import { fetchData } from '@/utils'
import MapChart from '@/components/MapChart.vue'

export default {
  components: {
    MapChart
  },
  data () {
    return {
      mapData: null
    }
  },
  async mounted () {
    try {
      this.mapData = await fetchData()
    } catch (err) {
      console.error(err)
      this.$message.error('数据请求失败')
    }
  }
}
</script>

<style scoped>
.home {
  padding: 20px;
}
</style>
