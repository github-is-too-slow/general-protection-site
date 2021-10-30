<template>
  <div class="header-container">
    <div class="header-logo-wrapper">
      <router-link to="/">
        <img class="header-logo"
             src="https://res.hc-cdn.com/cnpm-header-and-footer/2.0.6/base/header-china/components/images/logo.svg" />
      </router-link>
    </div>
    <div class="header-nav-wrapper">
      <ul class="header-nav">
        <li class="header-nav-item"
            @click="navItemClkHandler(1)">
          <router-link to="/"
                       :class="linkActive == 1 ? 'header-nav-item-active' : ''">交流专区</router-link>
        </li>
        <li class="header-nav-item"
            @click="navItemClkHandler(2)">
          <router-link to="/"
                       :class="linkActive == 2 ? 'header-nav-item-active' : ''">学习文档</router-link>
        </li>
        <li class="header-nav-item"
            @click="navItemClkHandler(3)">
          <router-link to="/"
                       :class="linkActive == 3 ? 'header-nav-item-active' : ''">敬请期待</router-link>
        </li>
      </ul>
    </div>
    <div class="header-tools-wrapper">
      <el-button type="primary" icon="el-icon-edit" size="small"
        style="margin-right: 20px" @click="writeNote">写博客</el-button>
      <div v-if="true"
           class="header-tools-login-register">
        <router-link to="/login"
                     class="header-tools-login">
          <el-link :underline="false">登录</el-link>
        </router-link>
        <router-link to="/register"
                     class="header-tools-register">
          <el-link :underline="false">注册</el-link>
        </router-link>
      </div>
      <div v-else
           class="header-tools-personal-center">
        <el-dropdown>
          <span class="el-dropdown-link">
            <el-avatar shape="square"
                       size="small"
                       :src="squareUrl"></el-avatar>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item icon="el-icon-plus">黄金糕</el-dropdown-item>
            <el-dropdown-item icon="el-icon-circle-plus">狮子头</el-dropdown-item>
            <el-dropdown-item icon="el-icon-circle-plus-outline">螺蛳粉</el-dropdown-item>
            <el-dropdown-item icon="el-icon-check">双皮奶</el-dropdown-item>
            <el-dropdown-item icon="el-icon-circle-check">蚵仔煎</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      linkActive: 1,
      squareUrl:
        'https://cube.elemecdn.com/9/c2/f0ee8a3c7c9638a54940382568c9dpng.png',
    }
  },
  methods: {
    navItemClkHandler(index) {
      this.linkActive = index
    },
    writeNote() {
      this.$router.push("/writeNote")
    }
  },
}
</script>

<style scoped>
.header-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 3%;
  min-width: 520px;
  height: 56px;
  font-size: 16px;
  border-bottom: 1px solid #dfe1e6;
}
.header-nav-item {
  display: inline-block;
  margin: 0 8px;
}
.header-nav-item-active {
  color: #262626;
  font-weight: 700;
  border-bottom: 2px solid red;
}
.header-tools-login {
  margin: 0 16px;
}
.header-nav-wrapper .router-link-active {
  color: #595959;
  padding: 17px 8px;
}
.header-nav-wrapper .router-link-active:hover {
  color: #262626;
}
.header-tools-wrapper {
  display: flex;
  align-items: center;
}
</style>
