<template>
  <div class="note-list-container">
    <el-card class="box-card" v-for="note in noteList" :key="note.id" shadow="hover">
      <a href="#" class="note-title" @click.prevent="showNoteDetail(note.id)">{{note.title}}</a>
      <p>{{note.abstract}}</p>
      <div class="note-tag-list">
        <span class="note-tag-item" v-for="tag in note.tagList" :key="tag.tagId">{{tag.tagName}}</span>
      </div>
      <div class="note-other-info">
        <div class="wrapper">
          <img class="img" style="width: 24px; height: 24px;"
                :src="note.author.avatar">
          <div class="text">{{note.author.name}}</div>
        </div>
        <el-tooltip class="note-count" effect="dark" content="阅读" placement="bottom">
          <span><i class="el-icon-view"></i> {{note.viewCount}}</span>
        </el-tooltip>
        <el-tooltip class="note-count" effect="dark" content="评论" placement="bottom">
          <span><i class="el-icon-s-comment"></i> {{note.commentCount}}</span>
        </el-tooltip>
        <el-tooltip class="note-count" effect="dark" content="赞" placement="bottom">
          <span><i class="el-icon-thumb"></i> {{note.statCount}}</span>
        </el-tooltip>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  props: {
    noteList: {
      type: Array,
      default: function () {
        return []
      }
    }
  },
  data () {
    return {

    }
  },
  methods: {
    showNoteDetail(noteId){
      console.log(noteId);
      this.$router.push("/noteDetail/" + noteId);
    }
  }
}
</script>

<style scoped>
.box-card {
  margin-bottom: 30px;
}
.note-title {
  font-size: 18px;
  font-weight: 700;
  color: #222226;
}
.note-title:hover {
  color: red;
  text-decoration: underline;
}
.note-tag-list {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}
.note-tag-item {
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
.note-tag-item:hover {
  background-color: #0969da;
  color: #fff;
}
.note-other-info {
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
.note-count {
  font-size: 12px;
  margin-left: 20px;
}
</style>