<template>
  <div class="dashboard">
    <el-row :gutter="20">
      <el-col :xs="24" :sm="12" :md="8" :lg="6">
        <el-card>
          <div slot="header" class="clearfix">
            <span>任务总数</span>
          </div>
          <div class="card-body">
            <h1>{{ totalTasks }}</h1>
          </div>
        </el-card>
      </el-col>
      <el-col :xs="24" :sm="12" :md="8" :lg="6">
        <el-card>
          <div slot="header" class="clearfix">
            <span>未完成任务</span>
          </div>
          <div class="card-body">
            <h1>{{ unfinishedTasks }}</h1>
          </div>
        </el-card>
      </el-col>
      <el-col :xs="24" :sm="12" :md="8" :lg="6">
        <el-card>
          <div slot="header" class="clearfix">
            <span>已完成任务</span>
          </div>
          <div class="card-body">
            <h1>{{ finishedTasks }}</h1>
          </div>
        </el-card>
      </el-col>
      <el-col :xs="24" :sm="12" :md="8" :lg="6">
        <el-card>
          <div slot="header" class="clearfix">
            <span>今日新增任务</span>
          </div>
          <div class="card-body">
            <h1>{{ todayTasks }}</h1>
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  data () {
    return {
      totalTasks: 0,
      unfinishedTasks: 0,
      finishedTasks: 0,
      todayTasks: 0
    }
  },
  mounted () {
    // 在这里获取数据并赋值给对应的 data 属性
    this.totalTasks = 50
    this.unfinishedTasks = 20
    this.finishedTasks = 30
    this.todayTasks = 10
  }
}
</script>

<style scoped>
.dashboard {
  margin: 20px;
}

.card-body {
  text-align: center;
  padding: 20px 0;
}
</style>
