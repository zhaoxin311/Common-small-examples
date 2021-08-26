<template>
  <div>
    <el-button type="primary" @click="addfrom">添加</el-button>
    <el-dialog
      :title="eldialog"
      :visible.sync="dialogVisible"
      width="50%"
      :close-on-click-modal="false"
      :before-close="handleClose"
      @opened="eldialingShow"
    >
      <div id="div1" class="toolbar" />
      <div style="padding: 5px 0; color: #ccc">中间隔离带</div>
      <div id="div2" class="text">
        <!--可使用 min-height 实现编辑区域自动增加高度-->
        <p>请输入内容</p>
      </div>
      <span>这是一段信息</span>
      <div>
        <Form id="form" />
      </div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button @click="dialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import E from "wangeditor";
import Form from "./components/form.vue";
export default {
  components: { Form },
  data() {
    return {
      eldialog: "",
      text: "",
      dialogVisible: false,
    };
  },
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
        // 富文本编辑器创建，获取节点
        const editor = new E("#div1", "#div2"); // 两个参数也可以传入 elem 对象，class 选择器
        editor.config.onchange = function (newHtml) {
          // that.editorContent即为最新的富文本内容
          that.editorContent = newHtml;
        };
        editor.destroy();
        editor.create();
        editor.txt.html(this.text);
      } else {
        this.textare = this.text;
        const that = this;
        const editor = new E("#div1", "#div2"); // 两个参数也可以传入 elem 对象，class 选择器
        this.textare.replace(/&lt;/g, "<").replace(/&gt;/g, ">");
        editor.config.onchange = function (newHtml) {
          // that.editorContent即为最新的富文本内容
          that.editorContent = newHtml;
        };
        editor.destroy();
        editor.create(); // 创建
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
    handleClose(done) {
      this.$confirm("确认关闭？")
        .then((_) => {
          done();
        })
        .catch((_) => {});
    },
  },
};
</script>

<style>
.toolbar {
  border: 1px solid #ccc;
}
.text {
  border: 1px solid #ccc;
  min-height: 400px;
}
</style>
