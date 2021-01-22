<template>
  <div>
    <el-form :model="ruleForm" ref="ruleForm" label-width="100px">
      <el-form-item label="阶段运动" prop="stage">
        <el-radio-group v-model="ruleForm.stage">
          <el-radio :label="true">是</el-radio>
          <el-radio :label="false">否</el-radio>
        </el-radio-group>
      </el-form-item>
      <div v-if="ruleForm.stage">
        <el-table :data="tableData" style="width: 100%" border>
          <el-table-column prop="date" label="日期" width="180"> </el-table-column>
          <el-table-column prop="name" label="姓名" width="180"> </el-table-column>
          <el-table-column prop="address" label="地址"> </el-table-column>
        </el-table>
      </div>
      <div v-else>
        <el-form-item label="运动时长" prop="type">
          <el-radio-group v-model="ruleForm.type">
            <el-radio label="custom">自定义</el-radio>
            <el-radio label="demo">demo</el-radio>
          </el-radio-group>
        </el-form-item>
        <div v-if="ruleForm.type === 'custom'">
          <el-form-item label="运动时长" prop="name">
            <el-input-number v-model="ruleForm.name" :min="1" :max="10" size="small" />
            秒
          </el-form-item>
          <el-form-item label="每秒提速" prop="name">
            <el-input-number v-model="ruleForm.name" :min="1" :max="10" size="small" />
            px
          </el-form-item>
          <el-form-item label="降速度临界点" prop="name">
            <el-input-number v-model="ruleForm.name" :min="1" :max="10" size="small" />
            秒
          </el-form-item>
          <el-form-item label="每秒减速" prop="name">
            <el-input-number v-model="ruleForm.name" :min="1" :max="10" size="small" />
            px
          </el-form-item>
        </div>
        <div v-else>
          <el-form-item label="案例" prop="demo">
            <el-radio-group v-model="ruleForm.demo">
              <el-radio label="lottery">抽奖</el-radio>
            </el-radio-group>
          </el-form-item>
        </div>
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')" size="small">立即创建</el-button>
          <el-button @click="resetForm('ruleForm')" size="small">重置</el-button>
        </el-form-item>
      </div>
    </el-form>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1517 弄",
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄",
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1516 弄",
        },
      ],
      ruleForm: {
        type: "custom",
        name: 1,
        demo: "lottery",
        stage: false,
      },
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid, a, b) => {
        if (valid) {
          console.log(this.ruleForm);
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
  },
};
</script>
