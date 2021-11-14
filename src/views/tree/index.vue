<template>
  <div>
    <el-button type="success" @click="addfrom">添  ddddd 加</el-button>

    <el-dialog
      :title="eldialog"
      :visible.sync="dialogVisible"
      width="50%"
      :close-on-click-modal="false"
      @opened="eldialingShow"
    >
      <div id="content" />
    </el-dialog>
  </div>
</template>

<script>
import E from "wangeditor";
export default {
  data() {
    return {
      eldialog: "",
      text: "",
      dialogVisible: false,
    };
  },
  created() {},
  methods: {
    // 打开弹出框
    addfrom() {
      // 清空之前的富文本内容
      this.text = "";
      // 更改弹出框的标题
      this.eldialog = "编辑富文本";
      // 显示富文本
      this.dialogVisible = true;
    },
    // 弹出框显现后的回调
    eldialingShow() {
      this.$nextTick(() => {
        this.fun1();
      });
    },
    // 富文本的事件
    fun1() {
      this.showif = true;
      // 先判断富文本是添加还是修改，
      // 如果this.text为空则是添加富文本内容，若是修改富文本的内容，只需要将之前的富文本内容赋给this.text即可
      if (this.text === "") {
        const that = this;
        const editor = new E(document.getElementById("content"));
        editor.config.onchange = function (newHtml) {
          // that.editorContent即为最新的富文本内容
          that.editorContent = newHtml;
        };
        editor.create();
        editor.txt.html(this.text);
      } else {
        this.textare = this.text;
        const that = this;
        const editor = new E(document.getElementById("content"));
        this.textare.replace(/&lt;/g, "<").replace(/&gt;/g, ">");
        editor.config.onchange = function (newHtml) {
          // that.editorContent即为最新的富文本内容
          that.editorContent = newHtml;
        };
        editor.create();
        this.textare = this.escape2Html(this.textare);
        editor.txt.html(this.textare);
      }
    },
    escape2Html(str) {
      str = str
        .replace(/&lt;/g, "<")
        .replace(/&gt;/g, ">")
        .replace(/&amp;/g, "&")
        .replace(/&quot;/g, '"')
        .replace(/&#39;/g, "'")
        .replace(/&npsp;/g, " ")
        .replace(/\n/g, "<br />")
        .replace(/\r/g, "<br />");
      return str;
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
