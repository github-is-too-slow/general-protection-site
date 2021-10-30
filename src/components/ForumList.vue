<template>
  <el-card class="box-card">
    <div slot="header"
         class="clearfix">
      <span>所有论坛</span>
    </div>
    <el-card v-for="forum in forumList"
         :key="forum.id"
         style="margin-bottom: 30px; cursor: pointer;"
         shadow="hover"
         >
      <div class="item" @click="viewDetail(forum.id)">
        <el-image
        style="width: 100px; height: 100px; vertical-align: bottom;"
        :src="forum.imgSrc"
        fit="contain"></el-image>
        <div class="forum-info" style="display: inline-block; heigth: 100%">
          <span>{{forum.name}}</span>
          <p class="forum-desc">
            {{forum.desc}}
          </p>
          <div class="bottom clearfix">
            <span>{{forum.sponer}}</span>
            发起于
            <span>{{forum.time}}</span>
          </div>
        </div>
      </div>
    </el-card>
  </el-card>
</template>

<script>
export default {
  name: 'ForumList',
  data() {
    return {
      forumList: [
        {
          id: 1,
          imgSrc: "https://img3m7.ddimg.cn/23/4/1229879597-1_e_1.jpg",
          name: '操作系统真相还原',
          desc: "本书从只有二十行的引导扇区代码出发，一步一步地向读者呈现一个操作系统框架的完成过程。书中不仅关注代码本身，",
          sponer: '李明',
          time: "2020/2/2"
        },
        {
          id: 2,
          imgSrc: "http://img60.ddimg.cn/digital/product/9/4/1901210904_cc_cover.jpg?version=a81f5c8e-45d7-4057-9ab3-0f75ab6db719",
          name: '操作系统真相还原',
          desc: "用诙谐幽默语言讲述的深入理解操作系统原理的精品 轻松自制操作系统 操作系统并不深奥 本书给予全新解读",
          sponer: '李明',
          time: "2020/2/2"
        }
      ],
    }
  },
  methods: {
    viewDetail(forumId){
      console.log(forumId);
      this.$router.push("/forumDetail/" + forumId);
    }
  }
}
</script>

<style scoped>

.item {
  display: flex;
  justify-content: space-between;

}
.forum-info {
  flex: auto;
}
.forum-desc {
  flex: auto;
  overflow: hidden;
}
.clearfix:before,
.clearfix:after {
  display: table;
  content: '';
}
.clearfix:after {
  clear: both;
}

</style>