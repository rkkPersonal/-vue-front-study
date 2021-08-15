<template>
  <el-table class="home-display" :data="tableData" border style="width: 100%">
    <el-table-column prop="name" label="姓名" width="120"> </el-table-column>
    <el-table-column prop="province" label="省份" width="120">
    </el-table-column>
    <el-table-column prop="city" label="市区" width="120"> </el-table-column>
    <el-table-column prop="address" label="地址" width="300"> </el-table-column>
    <el-table-column prop="zip" label="邮编" width="120"> </el-table-column>
    <el-table-column prop="email" label="邮箱" width="200"> </el-table-column>
    <el-table-column prop="date" label="日期" width="150"> </el-table-column>
    <el-table-column fixed="right" label="操作" width="100">
      <template slot-scope="scope">
        <el-button @click="handleClick(scope.row)" type="text" size="small"
          >查看</el-button
        >
        <!-- <el-button type="text" size="small">编辑</el-button> -->
        <!-- Form -->
        <el-button type="text" size="small" @click="dialogFormVisible = true"
          >编辑</el-button
        >

        <el-dialog
          title="用户信息"
          :visible.sync="dialogFormVisible"
          :append-to-body="true"
        >
          <el-form :model="form">
            <el-form-item label="姓名" :label-width="formLabelWidth">
              <el-input v-model="form.name" autocomplete="off"></el-input>
            </el-form-item>

            <el-form-item label="省份" :label-width="formLabelWidth">
              <el-input v-model="form.province" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="市区" :label-width="formLabelWidth">
              <el-input v-model="form.city" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="地址" :label-width="formLabelWidth">
              <el-input v-model="form.address" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="邮编" :label-width="formLabelWidth">
              <el-input v-model="form.zip" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="邮箱" :label-width="formLabelWidth">
              <el-input v-model="form.email" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="性别" :label-width="formLabelWidth">
              <el-select v-model="form.gender" placeholder="请选择性别">
                <el-option label="男" value="张三"></el-option>
                <el-option label="女" value="小花"></el-option>
              </el-select>
            </el-form-item>
          </el-form>
          <div slot="footer" class="dialog-footer">
            <el-button @click="dialogFormVisible = false">cancel</el-button>
            <el-button type="primary" @click="newUser()">submit </el-button>
          </div>
        </el-dialog>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      // dialogTableVisible: false,
      dialogFormVisible: false,
      form: {
        name: "",
        gender: "",
        address: "",
        email: "",
        city: "",
        province: "",
        zip: ""
      },
      formLabelWidth: "120px",
      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          province: "上海",
          city: "普陀区",
          address: "上海市普陀区金沙江路 1518 弄",
          zip: 200333,
          email: "1376969568@qq.com"
        }
      ]
    };
  },

  computed: {
    testComputed: function() {
      return this.tableData;
    }
  },
  mounted: function() {
    this.handleClick(); //method1 will execute at pageload
  },
  methods: {
    handleClick: function() {
      //以下代码也可以封装在函数中，在其他地方调用
      this.$axios
        .get("http://localhost:8081/getUserinfo", {})
        .then(response => {
          console.log(response.data.data);
          this.tableData = response.data.data;
        })
        .catch(function(error) {
          console.log(error);
        })
        .then(function() {
          // always executed
        });
    },
    newUser: function() {
      this.dialogFormVisible = false;
      console.log(this.form.name);
      var article = JSON.stringify({
        name: this.form.name,
        province: this.form.province,
        city: this.form.city,
        address: this.form.address,
        zip: this.form.zip,
        date: this.form.date,
        email: this.form.email
      });
      console.log(article);

      var url = "http://localhost:8081/add";
      axios
        .post(url, article, {
          headers: {
            "Content-Type": "application/json;charset=UTF-8"
          }
        })
        .then(res => {
          this.$message({
            message: res.data.message,
            type: "success"
          });
        })
        .catch(error => {
          this.$message({
            message: res.data.message,
            type: "error"
          });
        });
    }
  }
};
</script>
<style scoped>
@import url("//unpkg.com/element-ui@2.15.5/lib/theme-chalk/index.css");
</style>
