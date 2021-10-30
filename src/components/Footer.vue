<template>
  <div class="frient-link-container">
    <el-divider content-position="left">
      <span class="frient-link-title">友情链接</span>
    </el-divider>
    <ul class="frient-link-list">
      <li class="frient-link-item" v-for="linkItem in linkList" :key="linkItem.id">
        <el-link type="info" :href="linkItem.link" target="_blank">{{linkItem.name}}</el-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Footer",
  data () {
    return {
      linkList: [
        {
          id: 1,
          name: "哔哔哩哩",
          logo: require('../assets/img/bibilili.png'),
          link: "https://www.bilibili.com/"
        },
        {
          id: 2,
          name: "知乎",
          logo: require('../assets/img/zhihu.png'),
          link: "https://www.zhihu.com/"
        },
        {
          id: 3,
          name: "stackoverflow",
          logo: require('../assets/img/stackoverflow.png'),
          link: "https://stackoverflow.com/"
        },
      ]
    }
  }
}
</script>

<style scoped>
.frient-link-container {
  padding: 24px 3%;
}
.frient-link-list {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.frient-link-item {
  margin-right: 20px;
}
</style>