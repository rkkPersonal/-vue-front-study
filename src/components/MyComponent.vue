<template>
  <div class="container">
    <h1>
      重大新闻事件
    </h1>

    <ul>
      <li>{{ msg }}</li>
    </ul>
    <span>
      <el-input
        v-model="input"
        placeholder="请输入内容"
        size="small"
        style="width: 300px"
      ></el-input>
    </span>
    <span>
      <el-button type="primary" @click="search()" icon="el-icon-search"
        >搜索</el-button
      >
    </span>
    <home-page v-if="show == true"></home-page>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      msg: "唐山大地震！！！",
      show: false
    };
  },
  methods: {
    search() {
      this.show = true;
    }
  }
};
</script>
<style scoped>
@import url("//unpkg.com/element-ui@2.15.5/lib/theme-chalk/index.css");
</style>
