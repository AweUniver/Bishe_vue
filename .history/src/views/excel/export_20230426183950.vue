<template>
  <div class="container">
    <!-- 上传文件按钮 -->
    <div class="buttonBox1">
      <router-link to="/import">
        <el-tooltip content="数据采集页面" placement="top">
          <el-button type="primary" icon="el-icon-edit" circle></el-button>
        </el-tooltip>
      </router-link>
    </div>
    <div class="buttonBox">
      <router-link to="/home">
        <el-tooltip content="退出" placement="top">
          <el-button type="primary" icon="el-icon-s-home" circle></el-button>
        </el-tooltip>
      </router-link>
    </div>

    <!-- 搜索区域 -->
    <div class="searchBox">
      <el-input
        v-model="search"
        placeholder="基于编号模糊搜索"
        @change="searchHandle"
        clearable
      ></el-input>
      <el-button type="success" @click="submit" :disabled="disabled"
        >导出选中的数据</el-button
      >
    </div>

    <!-- 列表区域 -->
    <div class="tableBox">
      <el-table
        :data="tableData"
        :height="height"
        border
        style="width: 100%"
        v-loading="loading"
        element-loading-text="正在努力加载中..."
        @selection-change="selectionChange"
      >
        <el-table-column
          type="selection"
          width="50"
          align="center"
        ></el-table-column>
        <el-table-column
          prop="id"
          label="编号"
          min-width="10%"
        ></el-table-column>
        <el-table-column
          prop="name"
          label="检测杆"
          min-width="20%"
        ></el-table-column>
        <el-table-column
          prop="phone"
          label="未缺陷杆"
          min-width="20%"
        ></el-table-column>
        <el-table-column
          prop="bad"
          label="缺陷杆"
          min-width="20%"
        ></el-table-column>
        <el-table-column
          prop="time"
          label="创建时间"
          min-width="25%"
          :formatter="formatter"
        ></el-table-column>
      </el-table>
    </div>

    <!-- 分页区域 -->
    <div class="pageBox">
      <el-pagination
        background
        hide-on-single-page
        layout="total,sizes,prev,pager,next"
        :page-size="pageSize"
        :current-page="page"
        :total="total"
        @size-change="sizeChange"
        @current-change="prevNext"
        @prev-click="prevNext"
        @next-click="prevNext"
      >
      </el-pagination>
    </div>
  </div>
</template>

<script>
import xlsx from 'xlsx'
import { Loading } from 'element-ui'
import { formatTime } from '@/assets/js/utils'
export default {
  name: 'myHome',
  data () {
    return {
      tableData: [],
      loading: false,
      height: document.documentElement.clientHeight - 120,
      // 分页相关
      pageSize: 20,
      page: 1,
      total: 10,
      search: '',
      // 选中数据
      selectionList: [],
      disabled: false
    }
  },
  created () {
    this.queryData()
  },
  methods: {
    // 权限
    selectionChange (val) {
      this.selectionList = val
    },
    // 格式化
    formatter (row, col, val) {
      return formatTime(val, '{0}-{1}-{2} {3}:{4}:{5}')
    },
    // 获取数据
    queryData () {
      this.loading = true
      const data = window.localStorage.getItem('excel') || '[]'
      this.tableData = JSON.parse(data)
      this.loading = false
    },
    // 搜索按钮
    searchHandle (val) {
      this.page = val
      this.queryData()
    },
    // 分页出路
    sizeChange (val) {
      this.pageSize = val
      this.page = 1
      this.queryData()
    },
    prevNext (val) {
      this.page = val
      this.queryData()
    },
    // 导出数据
    submit () {
      if (this.selectionList.length <= 0) {
        return this.$message({
          message: '请您先选择要导出的数据库哦！',
          type: 'warning',
          showClose: true
        })
      }

      this.disabled = true
      const loading = Loading.service({
        text: '请您稍等片刻，正在处理中...',
        background: 'rgba(0,0,0,.5)'
      })

      const arr = this.selectionList.map(item => {
        return {
          编号: item.id,
          检测杆: item.name,
          缺陷杆: item.phone
        }
      })

      const sheet = xlsx.utils.json_to_sheet(arr)
      const book = xlsx.utils.book_new()

      xlsx.utils.book_append_sheet(book, sheet, 'Sheet1')
      xlsx.writeFile(book, `user${new Date().getTime()}.xls`)

      loading.close()
      this.disabled = false
    }
  }
}
</script>

<style lang="less" scoped>
.buttonBox1 {
  position: fixed;
  top: 10px;
  right: 80px;
  z-index: 9999;
}
.buttonBox {
  position: fixed;
  top: 10px;
  right: 20px;
  z-index: 9999;
}
.searchBox {
  padding: 20px;
  display: flex;
  justify-content: flex-start;
  & .el-input {
    width: 25%;
  }
  & .el-button {
    margin-left: 20px !important;
  }
}

.tableBox {
  padding: 0 15px;
}
</style>
