<template>
  <div class="container">
    <h1>
      重大新闻事件
      <el-button type="primary" @click="search()" icon="el-icon-search"
        >搜索</el-button
      >
    </h1>
    <ul>
      <li>{{ msg }}</li>
    </ul>
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
