<template>
  <div class="sidebar">
    <div class="sidebar-header">站点</div>
    <ul class="nav">
      <li v-for="site in sites" :key="site.id" @click="handleSiteClick(site.id)">
        {{ site.name }}
        <ul>
          <li v-for="pole in site.poles" :key="pole.id" @click="handlePoleClick(pole.id)">
            {{ pole.name }}
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data () {
    return {
      sites: [
        {
          id: 1,
          name: '站点1',
          poles: [
            { id: 1, name: '杆号1' },
            { id: 2, name: '杆号2' },
            { id: 3, name: '杆号3' }
          ]
        },
        {
          id: 2,
          name: '站点2',
          poles: [
            { id: 4, name: '杆号4' },
            { id: 5, name: '杆号5' },
            { id: 6, name: '杆号6' }
          ]
        }
      ]
    }
  },
  methods: {
    handleSiteClick (siteId) {
      // 处理站点点击事件
    },
    handlePoleClick (poleId) {
      // 处理杆号点击事件
    }
  }
}
</script>

<style>
.sidebar {
  width: 200px;
  height: 100%;
  border-right: 1px solid #ccc;
}

.sidebar-header {
  height: 30px;
  line-height: 30px;
  padding-left: 10px;
  background-color: #eee;
}

.nav {
  padding: 10px;
  list-style: none;
}

.nav li {
  cursor: pointer;
  margin-bottom: 10px;
}

.nav ul {
  padding-left: 20px;
  list-style: none;
}
</style>
