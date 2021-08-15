<template>
  <div>
    <table>
      <thead>
        <th>学生姓名</th>
        <th>课程</th>
      </thead>
      <tbody>
        <tr v-for="person in persons" :key="person.name">
          <td>{{ person.name }}</td>
          <td>{{ person.course }}</td>
        </tr>
      </tbody>
    </table>
    <input v-on:click="ajaxRequest" type="submit" name="提交" />
  </div>
</template>

<script>
export default {
  name: "Register",
  data: function () {
    return {
      persons: [
        {
          name: "steven",
          course: "english",
        },
        {
          name: "peck",
          course: "chinese",
        },
      ],
    };
  },
  methods: {
    ajaxRequest: function () {
      //以下代码也可以封装在函数中，在其他地方调用
      this.$axios.get("http://localhost:8081/user", {
          user: {
            username: 12345, //可选
          },
        })
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        })
        .then(function () {
          // always executed
          console.log("jjjj");
        });
    },
  },
};
</script>
