<template>
  <div>
    <!-- 顶部导航栏 -->
    <el-menu mode="horizontal" background-color="#fff" text-color="#333" active-text-color="#409EFF">
      <el-menu-item index="1">首页</el-menu-item>
      <el-menu-item index="2">产品</el-menu-item>
      <el-menu-item index="3">关于我们</el-menu-item>
    </el-menu>

    <!-- Banner图片 -->
    <div class="banner">
      <img src="/static/images/banner.jpg" alt="Banner">
    </div>

    <!-- 产品列表 -->
    <div class="product-list">
      <h2>我们的产品</h2>
      <ul>
        <li>
          <img src="/static/images/product1.jpg" alt="Product 1">
          <h3>产品1</h3>
          <p>产品1的介绍</p>
        </li>
        <li>
          <img src="/static/images/product2.jpg" alt="Product 2">
          <h3>产品2</h3>
          <p>产品2的介绍</p>
        </li>
        <li>
          <img src="/static/images/product3.jpg" alt="Product 3">
          <h3>产品3</h3>
          <p>产品3的介绍</p>
        </li>
      </ul>
    </div>

    <!-- 底部信息栏 -->
    <div class="footer">
      <p>版权所有 &copy; 2023-2025 XXX公司</p>
      <p>联系我们：XXX@XXX.com</p>
    </div>
  </div>
</template>

<style scoped>
  /* 顶部导航栏样式 */
  .el-menu {
    border-bottom: 1px solid #eee;
  }

  /* Banner图片样式 */
  .banner img {
    width: 100%;
  }

  /* 产品列表样式 */
  .product-list {
    margin: 50px auto;
    text-align: center;
  }

  .product-list h2 {
    font-size: 36px;
    margin-bottom: 30px;
  }

  .product-list ul {
    list-style: none;
    padding: 0;
    display: flex;
    justify-content: center;
  }

  .product-list li {
    margin: 0 30px;
    max-width: 300px;
    text-align: left;
  }

  .product-list li img {
    width: 100%;
  }

  .product-list li h3 {
    margin-top: 20px;
    font-size: 24px;
  }

  .product-list li p {
    margin-top: 10px;
    font-size: 16px;
    color: #666;
  }

  /* 底部信息栏样式 */
  .footer {
    background-color: #eee;
    text-align: center;
    padding: 20px 0;
    margin-top: 50px;
  }

  .footer p {
    margin: 5px 0;
    font-size: 14px;
    color: #666;
  }
</style>
