<template>
  <el-container style="height: 650px; border: 1px solid #eee">
    <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
      <el-menu
        @open="handleOpen"
        @close="handleClose"
        default-active="home"
        unique-opened
        router
      >
        <!-- <el-submenu index="1">
          <template slot="title"><i class="el-icon-menu"></i>站点名称</template>
          <el-menu-item index="2-1">杆号</el-menu-item>
          <el-menu-item index="2-2">杆号</el-menu-item>
          <el-menu-item index="2-3">杆号</el-menu-item>
          <el-menu-item index="2-4">杆号</el-menu-item>
          <el-menu-item index="2-5">杆号</el-menu-item>
          <el-menu-item index="2-6">杆号</el-menu-item>
          <el-menu-item index="2-7">杆号</el-menu-item>
          <el-menu-item index="2-8">杆号</el-menu-item>
          <el-menu-item index="2-9">杆号</el-menu-item>
          <el-menu-item index="2-10">杆号</el-menu-item>
          <el-menu-item index="2-11">杆号</el-menu-item>
          <el-menu-item index="2-12">杆号</el-menu-item>
          <el-menu-item index="2-13">杆号</el-menu-item>
          <el-menu-item index="2-14">杆号</el-menu-item>
          <el-menu-item index="2-15">杆号</el-menu-item>
          <el-menu-item index="2-16">杆号</el-menu-item>
          <el-menu-item index="2-17">杆号</el-menu-item>
        </el-submenu> -->
        <el-menu-item index="home">
          <i class="el-icon-menu"></i>
          <span slot="title">首页界面</span>
        </el-menu-item>
        <el-menu-item index="camera">
          <i class="el-icon-menu"></i>
          <span slot="title">任务分析界面</span>
        </el-menu-item>
        <el-menu-item index="charts">
          <i class="el-icon-menu"></i>
          <span slot="title">图表界面</span>
        </el-menu-item>
        <el-submenu index="3">
          <template slot="title">
            <i class="el-icon-menu"></i>
            <span>报表输出</span>
          </template>
          <el-menu-item index="import">导入数据</el-menu-item>
          <el-menu-item index="export">导出数据</el-menu-item>
        </el-submenu>
      </el-menu>
    </el-aside>

    <el-container class="main-container">
      <el-header style="text-align: right; font-size: 12px；">
        <!-- 右侧的菜单 -->
        <el-menu>
          <el-menu-item index="1" @click="logoutFn"
            ><i class="el-icon-switch-button"></i>退出</el-menu-item
          >
        </el-menu>
      </el-header>

      <el-main>
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  name: 'my-layout',
  data () {
    const item = {
      date: '',
      name: '',
      address: ''
    }
    return {
      tableData: Array(20).fill(item)
    }
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
          // 2. 跳转到地图页面
          this.$router.push('/date')
        })
        .catch((err) => err)
    },
    handleOpen (key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath)
    }
  }
}
</script>

<style lang="less" scoped>
.el-header {
  background-color: #b3c0d1;
  color: #333;
  line-height: 60px;
}

.el-aside {
  color: #333;
}

.main-container {
  height: 100%;
  .el-header,
  .el-aside {
    background-color: #b3c0d1;
  }
  .el-header {
    padding: 0;
    display: flex;
    flex-direction: row-reverse;
    // justify-content: space-between;
  }
  .el-main {
    overflow-y: scroll;
    height: 0;
    background-color: #f2f2f2;
  }
  .el-footer {
    background-color: #eee;
    font-size: 12px;
    // display: flex;
    // justify-content: center;
    // align-items: center;
  }
}
</style>
