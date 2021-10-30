<template>
  <div class="note-datail-container">
    <el-input class="note-title"
      type="textarea"
      placeholder="请输入文章标题（5 ~ 100个字）"
      v-model="note.title"
      maxlength="100"
      show-word-limit
      resize="none"
      :rows="2"
      >
    </el-input>
    <InnerMarkdown :editor="defaultEditor"/>
  </div>
</template>

<script>
import InnerMarkdown from '@/components/InnerMarkdown.vue'
export default {
  name: "NoteDetail",
  components: {
    InnerMarkdown
  },
  data () {
    return {
      note: {
        id: 1,
        title: '',
      },
      defaultEditor: {
        style:"height: 100vh;",
        value: "",
        toolbarsBackground: "#292d38",
        subfield: true,
        default_open: "edit",
        tabSize: 4,
        editable: true,
        toolbarsFlag: true ,
        toolbars: {
          bold: true, // 粗体
          italic: true, // 斜体
          header: true, // 标题
          underline: true, // 下划线
          strikethrough: true, // 中划线
          mark: true, // 标记
          superscript: true, // 上角标
          subscript: true, // 下角标
          quote: true, // 引用
          ol: true, // 有序列表
          ul: true, // 无序列表
          link: true, // 链接
          imagelink: true, // 图片链接
          code: true, // code
          table: true, // 表格
          fullscreen: true, // 全屏编辑
          readmodel: true, // 沉浸式阅读
          htmlcode: true, // 展示html源码
          help: true, // 帮助
          /* 1.3.5 */
          undo: true, // 上一步
          redo: true, // 下一步
          trash: true, // 清空
          save: true, // 保存（触发events中的save事件）
          /* 1.4.2 */
          navigation: true, // 导航目录
          /* 2.1.8 */
          alignleft: true, // 左对齐
          aligncenter: true, // 居中
          alignright: true, // 右对齐
          /* 2.2.1 */
          subfield: true, // 单双栏模式
          preview: true, // 预览
        }
      }
    }
  }
}
</script>

<style scoped>
.note-datail-container {
  padding: 0 24px;
}
.note-title {
  font-size: 18px;
  color: #222226;
  font-weight: 600;
  margin: 5px 0 20px;
}
</style>