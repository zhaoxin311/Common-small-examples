<template>
  <div class="rich-text">
    <ckeditor v-model="editorData" :config="editorConfig" />
    <p>{{ "富文本数据：" }}</p>
    <p>{{ editorData }}</p>
  </div>
</template>
<script>
import CKEditor from "ckeditor4-vue";

export default {
  components: { ckeditor: CKEditor.component },
  data() {
    return {
      editorData: "<p>为梦想灼伤了自己</p><p>也不要平庸的喘息</p>",
      editorConfig: {
        editorUrl: "https://your-website.example/ckeditor/ckeditor.js",
        // 编辑器的配置，参考：https://ckeditor.com/docs/ckeditor4/latest/guide/dev_vue.html
      },
    };
  },
};
</script>
