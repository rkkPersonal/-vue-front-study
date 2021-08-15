<template>
  <div class="container">
    <h1>重大新闻事件</h1>
    <ul>
      <li>{{ msg }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      msg: "唐山大地震！！！",
    };
  },
};
</script>