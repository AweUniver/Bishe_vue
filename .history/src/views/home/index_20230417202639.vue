<template>
  <div style="width:100%;height: 100%;">
  <iframe :src='src' frameborder="0" style="width:100%;height: 100%;"></iframe>
  </div>
</template>

<script>
// 模块内用命名导出的, 我把他们再收集起来形成对象, 放到echrats变量里
// import * as echarts from 'echarts'
export default {
  name: 'my-home',
  data () {
    return {
      showSessionId: '',
      src: ''
    }
  },
  mounted () {
    this.showSessionId = window.location.search;
    this.src=`@/`
  },
  methods: {

  }
}
</script>

<style lang="less" scoped>

</style>
