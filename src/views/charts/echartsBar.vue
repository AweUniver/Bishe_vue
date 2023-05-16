<template>
  <div
    class="echart"
    ref="mychart3"
    style="height:90%;width: 95%;"
  ></div>
</template>

<script>
import * as echarts from 'echarts'

export default {
  name: 'EchartsBar3',
  data () {
    return {}
  },
  mounted () {
    this.initBar()
  },
  methods: {
    initBar () {
      const option = {
        title: { // 标题组件
          text: '路线检测',
          top: 5,
          left: 'center', // 距离容器左侧的距离。可选left,right等
          textStyle: {
            color: '#fff',
            fontSize: 20
          }
        },
        grid: { // 直角坐标系内绘图网格
          containLabel: false,
          bottom: '10%', // grid 组件离容器下侧的距离。默认60px
          top: '20%' // grid 组件离容器上侧的距离。默认60px
        },
        legend: { // 图例组件
          top: '8%', // 图例组件离容器上侧的距离
          left: 'center', // 图例组件离容器左侧的距离
          textStyle: {
            color: '#fff',
            fontSize: 14
          },
          itemGap: 50, // 图例每项之间的间隔。默认10
          itemHeight: 10, // 图例标记的图形高度。默认14
          data: ['检测次数', '缺陷杆数']
        },
        xAxis: { // X轴-相关设置
          axisLabel: { // X轴-坐标轴刻度标签的相关设置。
            show: true,
            color: '#fff',
            margin: 20, // 刻度标签与轴线之间的距离。 默认8px
            fontSize: 15,
            interval: 0
          },
          axisTick: { // X轴-坐标轴刻度相关设置
            show: false
          },
          splitLine: { // X轴-分隔线
            show: false
          },
          axisLine: { // X轴-坐标轴轴线相关设置
            show: true,
            lineStyle: {
              color: '#384267',
              type: 'dashed' // 线的类型。可选'solid'等
            }
          },
          data: ['一月', '二月', '三月', '四月', '五月', '六月', '七月', '八月', '九月', '十月', '十一月', '十二月']
        },
        yAxis: [ // Y轴-相关设置
          { // 左侧y轴
            name: '检测次数',
            nameTextStyle: { // 坐标轴名称的文字样式
              color: '#fff',
              padding: [0, 0, 10, 0],
              fontSize: 14
            },
            axisLabel: { // Y轴-坐标轴刻度标签的相关设置
              fontSize: 14,
              color: '#fff'
            },
            axisTick: { // Y轴-坐标轴刻度相关设置。
              show: true,
              lineStyle: {
                color: '#384267'
              }
            },
            splitLine: { // Y轴-分隔线
              show: true,
              lineStyle: {
                color: '#384267',
                type: 'dashed'
              }
            },
            axisLine: { // Y轴-坐标轴轴线相关设置。
              show: true,
              lineStyle: {
                color: '#384267',
                type: 'solid'
              }
            }
          },
          { // 右侧y轴
            position: 'right', // y 轴的位置。可选left,right。默认 第一个 y 轴在左侧（'left'），第二个 y 轴在另一侧。
            axisLabel: { // Y轴-坐标轴刻度标签的相关设置
              show: true,
              textStyle: {
                fontSize: 14,
                color: '#fff'
              }
            },
            axisTick: { // Y轴-坐标轴刻度相关设置。
              show: false
            },
            splitLine: { // Y轴-分隔线
              show: false
            },
            axisLine: { // Y轴-坐标轴轴线相关设置。
              show: true,
              lineStyle: {
                color: '#384267',
                type: 'solid'
              }
            }
          }
        ],
        series: [
          { // 柱状系列数据
            name: '检测次数',
            type: 'bar',
            yAxisIndex: 0, // 使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用
            data: [1000, 750, 850, 500, 233, 1000, 750, 850, 500, 233, 1000, 750],
            barWidth: 30,
            itemStyle: {
              color: {
                type: 'linear',
                x: 0,
                y: 0,
                x2: 0,
                y2: 1,
                global: false,
                colorStops: [
                  { offset: 0, color: '#057DFE' }, // 0% 处的颜色
                  { offset: 1, color: '#02D7EA' }// 100% 处的颜色
                ]
              }
            },
            label: { // 图形上的文本标签
              show: true,
              position: 'top', // 标签的位置。可选top，left等
              distance: 10, // 距离图形元素的距离。默认值5
              color: '#fff'
            }
          },
          { // 折线系列数据
            name: '缺陷杆数',
            type: 'line',
            data: [1230, 500, 650, 350, 233, 1230, 500, 650, 350, 233, 350, 233],
            // 使用的 y 轴的 index
            // 在单个图表实例中存在多个 y轴的时候有用
            yAxisIndex: 1,
            smooth: false, // 是否平滑曲线显示
            // 标记的图形为实心圆。可选 'circle'，'rect'等
            symbol: 'emptyCircle',
            symbolSize: 10, // 标记的大小
            itemStyle: {
              // 折线拐点标志的样式
              color: '#FF9B61'
            },
            lineStyle: {
              color: '#FF9B61'
            }
          }
        ],
        tooltip: {
          trigger: 'axis',
          backgroundColor: 'rgba(17,95,182,0.5)',
          textStyle: {
            color: '#fff'
          },
          formatter: (params) => {
            const oneDotHtml = '<span style="display:inline-block;margin-right:5px;width:10px;height:10px;background-color:#057DFE"></span>'
            const twoDotHtml = '<span style="display:inline-block;margin-right:5px;width:10px;height:10px;background-color:#FF9B61"></span>'
            return (
              `${params[0].name}<br />
            ${oneDotHtml}${params[0].seriesName}：${params[0].value}<br />
            ${twoDotHtml}${params[1].seriesName}：${params[1].value}
            `
            )
          }
        }
      }
      const myChart = echarts.init(this.$refs.mychart3)
      myChart.setOption(option)
    }
  }
}

</script>
<style scoped>
</style>
