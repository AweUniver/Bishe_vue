<template>
  <div class="container">
    <el-row>
      <el-col :span="8">
        <!-- 左侧侧边栏 -->
        <div class="sidebar">
          <div class="sidebar-header">站点</div>
          <el-tree :data="sites" :props="treeProps" @node-click="handleNodeClick" />
        </div>
      </el-col>
      <el-col :span="16">
        <div class="content">
          <!-- 右侧上方按钮和标签栏 -->
          <el-row class="toolbar">
            <el-col :span="24">
              <el-button-group>
                <el-button v-for="part in parts" :key="part.id" type="primary" @click="handlePartClick(part.id)">
                  {{ part.name }}
                </el-button>
              </el-button-group>
            </el-col>
          </el-row>
          <el-tabs v-model="activeName" @tab-click="handleTabClick">
            <el-tab-pane v-for="part in parts" :key="part.id" :label="part.name" :name="part.id">
              {{ part.content }}
            </el-tab-pane>
          </el-tabs>
          <!-- 右侧下方显示图片 -->
          <div class="canvas-container">
            <canvas ref="canvas"></canvas>
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  data () {
    return {
      activeName: 'part1',
      sites: [
        {
          id: 1,
          name: '站点1',
          children: [
            { id: 1, name: '杆号1' },
            { id: 2, name: '杆号2' },
            { id: 3, name: '杆号3' }
          ]
        },
        {
          id: 2,
          name: '站点2',
          children: [
            { id: 4, name: '杆号4' },
            { id: 5, name: '杆号5' },
            { id: 6, name: '杆号6' }
          ]
        }
      ],
      parts: [
        { id: 'part1', name: '部位1', content: '部位1的内容' },
        { id: 'part2', name: '部位2', content: '部位2的内容' },
        { id: 'part3', name: '部位3', content: '部位3的内容' }
      ],
      treeProps: {
        label: 'name',
        children: 'children'
      }
    }
  },
  methods: {
    handleNodeClick (data) {
      // 处理节点点击事件
    },
    handlePartClick (partId) {
      // 处理部位按钮点击事件
    },
    handleTabClick (tab) {
      // 处理标签页点击事件
    }
  },
  mounted () {
    // 初始化canvas
    const canvas = this.$refs.canvas
    // ...
  }
}
</script>

<style scoped>
.container {
  padding: 20px;
}

.sidebar {
  background-color: #f2f2f2;
  border: 1px solid #dcdfe6;
  border-radius: 4px;
  padding: 10px;
}

.sidebar-header {
  font-size:
}
