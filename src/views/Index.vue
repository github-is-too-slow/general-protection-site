<template>
  <el-container>
    <el-header>
      <Header/>
    </el-header>
    <el-main>
      <router-view/>
    </el-main>
    <el-footer>
      <Footer/>
    </el-footer>
  </el-container>
</template>

<script>
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'

export default {
  name: 'Index',
  components: {
    Header,
    Footer
  }
}
</script>

<style scoped>
.el-header {
  padding: 0;
}
.el-main {
  width: 80%;
  margin: 0 auto;
  margin-bottom: 40px;
}
</style>