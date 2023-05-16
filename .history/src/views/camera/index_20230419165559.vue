<template>
  <el-container style="height: 650px; border: 1px solid #eee">
  <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
    <el-menu :default-openeds="['1', '3']">
      <el-menu-item >
          <i class="el-icon-menu"></i>
          <span slot="title">任务分析</span>
        </el-menu-item>
    </el-menu>
  </el-aside>

  <el-container class="main-container">
    <el-header style="text-align: right; font-size: 12px；">
      <!-- 右侧的菜单 -->
      <el-menu
      >
        <el-menu-item index="1" @click="logoutFn"
          ><i class="el-icon-switch-button"></i>退出</el-menu-item
        >
      </el-menu>
    </el-header>

    <el-main>
      图片位置
      <router-view></router-view>
    </el-main>
  </el-container>
</el-container>
</template>

<script>
// import { mapGetters } from 'vuex'
// import { getMenusAPI } from '@/api'
// export default {
//   name: 'my-layout',
//   computed: {
//     ...mapGetters(['nickname', 'username', 'user_pic'])
//   },
//   data () {
//     return {
//       menus: [] // 侧边栏数据
//     }
//   },
//   created () {
//     this.getMenusListFn()
//   },
//   methods: {
//     // 退出登录
//     logoutFn () {
//       // 询问用户是否退出登录
//       this.$confirm('您确认退出登录吗？', '提示', {
//         confirmButtonText: '确定',
//         cancelButtonText: '取消',
//         type: 'warning'
//       })
//         .then(() => {
//           // TODO：执行退出登录的操作
//           // 1. 清空 token
//           this.$store.commit('updateToken', '')
//           // 2. 跳转到登录页面
//           this.$router.push('/date')
//         })
//         .catch((err) => err)
//     },
//     // 获取侧边栏菜单数据
//     async getMenusListFn () {
//       const { data: res } = await getMenusAPI()
//       console.log(res)
//       this.menus = res.data
//     }
//   }
// }
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
    // 退出登录
    logoutFn () {
      // 询问用户是否退出
      this.$confirm('您确认退出吗？', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          // TODO：执行退出登录的
          // 1. 清空 token
          this.$store.commit('updateToken', '')
          // 2. 跳转到登录页面
          this.$router.push('/home')
        })
        .catch((err) => err)
    }
  }
}
</script>

<style lang="less" scoped>

.el-header {
    background-color: #B3C0D1;
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
    background-color: #B3C0D1;
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
