<template>
  <div id="app">
    <div class="echarts-wrap">
      <!--折线柱状图 -->
      <echarts-bar class="echarts-item"></echarts-bar>
      <div class="back"><el-button  type="primary" size="small" @click="logoutFn">退出</el-button></div>
    </div>

  </div>
</template>

<script>
import echartsBar from '@/views/charts/echartsBar'
export default {
  name: 'App',
  components: {
    echartsBar
  },
  methods: {
    // 退出
    logoutFn () {
      // 询问用户是否退出
      this.$confirm('您确认退出吗？', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          // TODO：执行退出的操作
          // 1. 清空 token
          this.$store.commit('updateToken', '')
          // 2. 跳转到首页
          this.$router.push('/home')
        })
        .catch((err) => err)
    }
  }
}
</script>

<style>
html,
body {
  height: 100%;
  width: 100%;
  padding: 0;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #0e3d52;
  height: 100%;
  width: 100%;
  overflow-x: hidden;
}
.echarts-wrap {
  height: 100%;
  width: 100%;
  display: flex;
  flex-wrap: wrap;
}
.echarts-item {
  width: 50%;
}
.back{
  /* display: flex; */
  color: aliceblue;
  height: 40px;
  text-align:center
}
.buttonBox {
  position: fixed;
  top: 0px;
  right: 0px;
  z-index: 9999;
}
</style>
