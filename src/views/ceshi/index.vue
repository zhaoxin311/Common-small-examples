<template>
  <div class="hello">
    <!-- <button @click="gettwo()">点击</button> -->
    <div id="div1" class="toolbar" />

    <div style="padding: 5px 0; color: #ccc">中间隔离带</div>

    <div id="div2" class="text">
      <!--可使用 min-height 实现编辑区域自动增加高度-->
      <p>请输入内容</p>
    </div>

    <div id="div3">
      <p>第二个 demo（常规）</p>
    </div>
  </div>
</template>

<script>
import E from "wangeditor";

export default {
  // data () {
  //   return {
  //   }
  // },
  // methods: {
  //   gettwo(){
  //     shuchu();
  //   }
  // },
  mounted() {
    var editor1 = new E("#div1", "#div2"); // 两个参数也可以传入 elem 对象，class 选择器
    editor1.create();

    var editor2 = new E("#div3");
    editor2.create();
  },
};
</script>

<style scoped>
toolbar {
  border: 1px solid #ccc;
}
.text {
  border: 1px solid #ccc;
  height: 400px;
}
#div3 {
  margin-top: 50px;
}
</style>
