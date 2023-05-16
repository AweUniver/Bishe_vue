<template>
  <el-container style="height: 650px; border: 1px solid #eee">
    <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
      <el-menu>
        <el-menu-item>
          <i class="el-icon-menu"></i>
          <span slot="title">站点</span>
        </el-menu-item>
      </el-menu>
      <el-row>
          <el-button autofocus style="margin-left: 10px; width:98.91px">相关杆1</el-button>
          <el-button style="width:98.91px">相关杆2</el-button>
          <el-button style="width:98.91px">相关杆3</el-button>
          <el-button style="width:98.91px">相关杆4</el-button>
          <el-button style="width:98.91px">相关杆5</el-button>
          <el-button style="width:98.91px">相关杆6</el-button>
          <el-button style="width:98.91px">相关杆7</el-button>
          <el-button style="width:98.91px">相关杆8</el-button>
          <el-button style="width:98.91px">相关杆9</el-button>
          <el-button style="width:98.91px">相关杆10</el-button>
          <el-button style="width:98.91px">相关杆11</el-button>
          <el-button style="width:98.91px">相关杆12</el-button>
          <el-button style="width:98.91px">相关杆13</el-button>
          <el-button style="width:98.91px">相关杆14</el-button>
          <el-button style="width:98.91px">相关杆15</el-button>
        </el-row>
    </el-aside>

    <el-container class="main-container">
      <el-header style="text-align: right; font-size: 12px；">
        <!-- 右侧的菜单 -->
        <el-row>
          <el-button >相关部位1</el-button>
          <el-button>相关部位2</el-button>
          <el-button>相关部位3</el-button>
          <el-button>相关部位4</el-button>
          <el-button>相关部位5</el-button>
          <el-button>相关部位6</el-button>
          <el-button>相关部位7</el-button>
          <el-button>相关部位8</el-button>
          <el-button type="danger" @click="logoutFn"
            ><i class="el-icon-switch-button"></i>退出</el-button
          >
        </el-row>
      </el-header>

      <el-main>
        <div class="container">
          <div class="canvasBox">
            <canvas
              ref="canvasRef"
              :width="canvasWidth"
              :height="canvasHeight"
            ></canvas>
          </div>
        </div>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  name: 'my-layout',
  data () {
    return {
      weight: '',
      canvasHeight: 588,
      canvasWidth: 1030,
      ctx: null
    }
  },
  mounted () {},
  methods: {

    // 初始化canvas画图函数
    init: function () {
      this.ctx = this.$refs.canvasRef.getContext('2d')
    },

    // 退出
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
.container {
  height: 588px;
  width: 1030px;
  padding: 0px;
  margin: 0px;
}
.canvasBox {
  overflow: hidden;
  width: 1030px;
  height: 588px;
  background-color: #fff;
  border-radius: 3px;
  position: absolute;
  left: 58.1%;
  top: 55%;
  transform: translate(-50%, -50%);
  padding: 0 30px;
  box-sizing: border-box;
}
canvas {
  // transform: scale(.5);
  width: 1030px;
  height: 588px;
  border: 1px solid;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
