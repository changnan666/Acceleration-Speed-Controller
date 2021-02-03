<template>
  <div class="container">
    <div class="controller">
      <el-form :model="ruleForm" ref="ruleForm" label-width="100px">
        <el-form-item label="运动总时长" prop="allTime">
          <el-input-number v-model="ruleForm.allTime" :min="1" size="small" /> 秒
        </el-form-item>
        <el-form-item label="无限循环" prop="loop">
          <el-switch v-model="ruleForm.loop" />
        </el-form-item>
        <el-form-item label="循环往复" prop="loopBack">
          <el-switch v-model="ruleForm.loopBack" />
        </el-form-item>
        <el-form-item v-show="ruleForm.loop || ruleForm.loopBack" label="循环间隔时间" prop="interval">
          <el-input-number v-model="ruleForm.interval" size="small" /> 秒
        </el-form-item>
        <el-table :data="ruleForm.stageTime" size="small" border style="width: 100%">
          <el-table-column label="时间段（毫秒）" width="300">
            <template #default="scoped">
              <div class="time">
                <el-form-item>
                  <el-input v-model="scoped.row.start" size="small" type="number" />
                </el-form-item>
                <span>至</span>
                <el-form-item>
                  <el-input v-model="scoped.row.end" size="small" type="number" />
                </el-form-item>
              </div>
            </template>
          </el-table-column>
          <el-table-column prop="css" label="执行动作（css）" width="300">
            <template #default="scoped">
              <css-editor />
            </template>
          </el-table-column>
        </el-table>
      </el-form>
      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')" size="small">添加时间段</el-button>
        <el-button @click="resetForm('ruleForm')" size="small">重置</el-button>
      </el-form-item>
    </div>
    <div class="play-container">123</div>
  </div>
</template>

<script>
import cssEditor from "./cssEditor.vue";

export default {
  name: "App",
  components: {
    cssEditor,
  },
  data() {
    return {
      ruleForm: {
        allTime: 1,
        interval: 0,
        loop: false,
        loopBack: false,
        stageTime: [
          {
            start: 0,
            end: 1000,
            css: "666",
          },
        ],
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


<style scoped>
.container {
  display: flex;
}

.container .time {
  display: flex;
  justify-content: center;
  align-items: center;
}

.container .time span {
  margin: 0 10px;
}
</style>

<style>
.container .time .el-form-item__content {
  margin: 0 !important;
}

.container .time .el-form-item {
  margin: 0;
}

.container .time .el-input--small .el-input__inner {
  padding-right: 0;
}
</style>