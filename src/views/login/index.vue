<template>
  <div class="login-content">
    <div class="left-box">欢迎光临</div>
    <div class="right-box">
      <div class="txt">
        <h1>欢迎回来</h1>
        <p>账号密码登录</p>
        <el-form ref="form" :model="loginForm" :rules="rules">
          <el-form-item prop="username">
            <el-input
              placeholder="请输入用户名"
              type="text"
              v-model.trim="loginForm.username"
            />
          </el-form-item>
          <el-form-item prop="password">
            <el-input
              placeholder="请输入密码"
              type="password"
              v-model.trim="loginForm.password"
            />
          </el-form-item>
          <el-form-item>
            <el-button class="fromButton" type="primary" @click="onSubmit"
              >登录</el-button
            >
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'
import rules from './rules'
const loginForm = reactive({
  username: '',
  password: ''
})

// 登录
const onSubmit = () => {
  console.log('submit!')
}
</script>
<style lang="scss" scoped>
.login-content {
  width: 100%;
  height: 100vh;
  display: flex;
  .left-box {
    width: 66%;
    background-color: #6366f1;
    text-align: center;
    line-height: 100vh;
    font-size: 58px;
    font-weight: 900;
    color: #fff;
  }
  .right-box {
    height: 100vh;
    width: 34%;
    .txt {
      text-align: center;
      width: 300px;
      margin-left: 110px;
      height: 50vh;
      margin-top: 30vh;
      h1,
      p {
        padding-bottom: 20px;
      }
      p {
        color: #bbc0d0;
      }
      .fromButton {
        background-color: #626aef;
        width: 100%;
        border-radius: 20px;
      }
    }
  }
}
</style>
