<template>
  <div class="content">
    <div class="login">
      <div class="title">
        <h2>登录</h2>
      </div>
      <el-form ref="ruleFormRef" :model="ruleForm" status-icon :rules="rule">
        <el-form-item label="邮箱" prop="email">
          <el-input v-model="ruleForm.email" />
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input v-model="ruleForm.password" type="password" autocomplete="off" />
        </el-form-item>
        <div class="foot">
          <el-checkbox v-model="ruleForm.check" size="large" />
          <span>勾选后则视为同意平台的用户协议</span>
        </div>
        <el-button style="width: 400px;" type="primary">登录</el-button>
      </el-form>
      <p class="reg-text">需要新的账号？点击 <span>注册</span></p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const ruleFormRef = ref(null)
const ruleForm = ref({
  email: '',
  password: '',
  check: false
})

const validatorEmail = (rule, value, callback) => {
  if (value === '') {
    callback(new Error('请填写您的email'))
    return
  }
  else {
    callback()
  }
}
const validatorPassword = (rule, value, callback) => {
  if (value === '') {
    callback(new Error('请填写您的密码'))
    return
  }
  else {
    callback()
  }
}
const validatorCheck = (rule, value, callback) => {
  if (value !== true) {
    callback(new Error('请勾选用户协议'))
    return
  }
  else {
    callback()
  }
}

const rule = ref({
  email: [{ validator: validatorEmail, trigger: 'blur' }],
  password: [{ validator: validatorPassword, trigger: 'blur' }],
  check: [{ validator: validatorCheck, trigger: 'blur' }],
})


</script>

<style lang="scss" scoped>
.content {
  width: 100%;
  height: 100vh;
  display: flex;

}

.login {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #f1f1f1;
  padding: 0px 60px;

  h2 {
    font-size: 20;
    font-weight: 400;
  }

  .foot {
    display: flex;
    justify-content: center;
    align-items: center;

    span {
      margin-left: 10px;
    }
  }

  .reg-text {
    font-size: 13px;

    span {
      padding: 2px 3px;
      cursor: pointer;
      border-radius: 3px;
      transition: background-color ease-in 0.1s;

      &:hover {
        background-color: #d5d5d5;
      }

      &:active {
        background-color: #b8b8b8;
      }
    }
  }


}
</style>
