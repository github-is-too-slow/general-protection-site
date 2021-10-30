<template>
  <div class="question-container">
    <el-card class="box-card" v-for="question in questionList" :key="question.id" shadow="hover">
      <a href="#" class="question-title">{{question.title}}</a>
      <p>{{question.abstract}}</p>
      <div class="question-tag-list">
        <span class="question-tag-item" v-for="tag in question.tagList" :key="tag.tagId">{{tag.tagName}}</span>
      </div>
      <div class="question-other-info">
        <div class="wrapper">
          <img class="img" style="width: 24px; height: 24px;"
                :src="question.author.avatar">
          <div class="text">{{question.author.name}}</div>
        </div>
        <el-tooltip class="question-count" effect="dark" content="阅读" placement="bottom">
          <span><i class="el-icon-view"></i> {{question.viewCount}}</span>
        </el-tooltip>
        <el-tooltip class="question-count" effect="dark" content="评论" placement="bottom">
          <span><i class="el-icon-s-comment"></i> {{question.commentCount}}</span>
        </el-tooltip>
        <el-tooltip class="question-count" effect="dark" content="赞" placement="bottom">
          <span><i class="el-icon-thumb"></i> {{question.statCount}}</span>
        </el-tooltip>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  props: {
    questionList: {
      type: Array,
      default: function () {
        return []
      }
    }
  },
  data () {
    return {

    }
  }
}
</script>

<style scoped>
.box-card {
  margin-bottom: 30px;
}
.question-title {
  font-size: 18px;
  font-weight: 700;
  color: #222226;
}
.question-title:hover {
  color: red;
  text-decoration: underline;
}
.question-tag-list {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}
.question-tag-item {
  color: #0969da;
  padding: 0 8px;
  border: 1px solid #fff;
  margin-bottom: 4px;
  border-radius: 2em;
  background-color: #ddf4ff;
  font-weight: 500;
  font-size: 12px;
  line-height: 22px;
  cursor: pointer;
}
.question-tag-item:hover {
  background-color: #0969da;
  color: #fff;
}
.question-other-info {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.wrapper{
    /* background: #cc8548; */
    /* padding: 20px; */
    display: flex;
    flex-direction: row;
    align-items: center; /*垂直居中*/
    justify-content: flex-start; /*水平居中*/
    font-size: 0;
}
.img{
    vertical-align: middle;
    align-items: center;
}
.text{
    padding-left: 5px;
    font-size: 12px;
}
.question-count {
  font-size: 12px;
  margin-left: 20px;
}
</style>