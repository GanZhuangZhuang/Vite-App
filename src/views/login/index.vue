<template>
  <el-row class="login-container">
    <el-col :lg="16" :md="12" :span="24" class="left">
      <div>欢迎光临</div>
    </el-col>
    <el-col :lg="8" :md="12" :span="24" class="right">
      <h2 class="title">欢迎回来</h2>
      <div>
        <div class="line"></div>
        <div>账号密码登录</div>
        <div class="line"></div>
      </div>
      <el-form ref="formRef" :model="loginForm" :rules="rules">
        <el-form-item prop="username">
          <el-input
            v-model="loginForm.username"
            placeholder="请输入用户名"
            @keyup.enter="handleLogin"
          >
            <template #prefix>
              <el-icon>
                <User />
              </el-icon>
            </template>
          </el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input
            v-model="loginForm.password"
            placeholder="请输入密码"
            show-password
            type="password"
            @keyup.enter="handleLogin"
          >
            <template #prefix>
              <el-icon>
                <Lock />
              </el-icon>
            </template>
          </el-input>
        </el-form-item>
        <el-form-item>
          <el-button
            :loading="loading"
            color="#626aef"
            round
            @click="handleLogin"
            >登录</el-button
          >
        </el-form-item>
      </el-form>
    </el-col>
  </el-row>
</template>

<script setup>
import { reactive, ref } from 'vue'
import rules from './rules'
import { useStore } from 'vuex'
const loading = ref(false)
const store = useStore()
const formRef = ref(null)
const loginForm = reactive({
  username: 'admin',
  password: 'admin'
})
const handleLogin = async () => {
  try {
    loading.value = true
    await formRef.value.validate()
    await store.dispatch('user/login', loginForm)
  } catch (e) {
    console.log(e, 'login')
  } finally {
    loading.value = false
  }
}
</script>

<style lang="scss" scoped>
.login-container {
  --tw-bg-opacity: 1;
  background-color: rgba(99, 102, 241, var(--tw-bg-opacity));
  min-height: 100vh;
  .left {
    display: flex;
    justify-content: center;
    align-items: center;
    div {
      font-weight: 700;
      font-size: 3rem;
      line-height: 1;
      margin-bottom: 1rem;
      --tw-text-opacity: 1;
      color: rgba(253, 253, 253, var(--tw-text-opacity));
    }
  }
  .right {
    display: flex;
    align-items: center;
    justify-content: center;
    --tw-bg-opacity: 1;
    background-color: rgba(253, 253, 253, var(--tw-bg-opacity));
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
    -ms-flex-direction: column;
    -webkit-flex-direction: column;
    flex-direction: column;
    .el-form {
      width: 250px;
      .el-button {
        width: 100%;
      }
    }
    .title {
      font-weight: 700;
      font-size: 1.875rem;
      line-height: 2.25rem;
      --tw-text-opacity: 1;
      color: rgba(31, 41, 55, var(--tw-text-opacity));
    }
    & > div {
      display: flex;
      -webkit-box-align: center;
      align-items: center;
      justify-content: center;
      margin-top: 1.25rem;
      margin-bottom: 1.25rem;
      --tw-text-opacity: 1;
      color: rgba(209, 213, 219, var(--tw-text-opacity));
      .line {
        --tw-bg-opacity: 1;
        background-color: rgba(229, 231, 235, var(--tw-bg-opacity));
        height: 1px;
        width: 4rem;
      }
    }
  }
}
</style>
