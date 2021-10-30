<template>
  <div class="editor">
    <mavon-editor :style="editor.style"
      :value="editor.value" :toolbarsBackground="editor.toolbarsBackground"
      :subfield="editor.subfield" :default_open="editor.default_open"
      :tabSize="editor.tabSize" :editable="editor.editable"
      :toolbarsFlag="editor.toolbarsFlag" :toolbars="editor.toolbars"></mavon-editor>
  </div>
</template>

<script>
import { mavonEditor } from 'mavon-editor'
import 'mavon-editor/dist/css/index.css'

export default {
  name: "InnerMarkdown",
  components: {
    'mavon-editor': mavonEditor
  },
  props: {
    editor: {
      type: Object,
      default: function(){
        return null;
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
</style>