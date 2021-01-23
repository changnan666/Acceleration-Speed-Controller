<template>
  <el-form :model="ruleForm" ref="ruleForm" label-width="100px">
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
  </el-form>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
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
