<template>
  <div class="login-area">
    <div class="top-banner-area">
      <div class="top-banner">
        <img src="../assets/img/register.png">
      </div>
    </div>
    <div class="login-box">
      <el-divider>登录</el-divider>
      <el-form :model="loginDate"
               status-icon
               :rules="rules"
               ref="ruleForm"
               class="demo-ruleForm"
               size="small">
        <el-form-item prop="email">
          <el-input v-model="loginDate.email"
                    placeholder="登录邮箱"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input type="password"
                    placeholder="密码"
                    v-model="loginDate.password"
                    autocomplete="off"></el-input>
        </el-form-item>
        <div class="login-tool">
          <el-button type="primary"
                     @click="submitForm('ruleForm')">登录</el-button>
        </div>
        <div class="to-register">
          <el-popover placement="left"
                      title="忘记密码这么办？"
                      width="250"
                      trigger="hover"
                      content="如果您忘记了密码，请联系管理员邮箱：1336077509@qq.com">
            <el-link slot="reference" :underline="false">忘记密码？</el-link>
          </el-popover>
          <router-link to="/register">
            <el-link :underline="false">没有账号？前去注册 <i class="el-icon-arrow-right"></i></el-link>
          </router-link>
        </div>
      </el-form>

    </div>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    var checkEmail = (rule, value, callback) => {
      if (!value) {
        return callback(new Error('注册邮箱不能为空'))
      }
      const emailRegExp = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
      if (emailRegExp.test(value)) {
        callback()
      } else {
        callback(new Error('邮箱不合法'))
      }
    }
    return {
      loginDate: {
        email: '',
        password: '',
      },
      rules: {
        email: [{ validator: checkEmail, trigger: 'blur' }],
        password: [{ required: true, message: '请输入密码', trigger: 'blur' }],
      },
    }
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          // 通过验证规则，开始注册
          alert('submit!')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
  },
}
</script>

<style scoped>
.top-banner-area {
  background: #00a0d8;
  height: 86px;
  text-align: center;
  margin-bottom: 20px;
}
.login-box {
  width: 80%;
  margin: 20px auto;
}
.el-divider__text {
  font-size: 38px;
}
.el-form {
  width: 420px;
  margin: 60px auto;
}
.el-checkbox-group {
  text-align: left;
}
.login-tool {
  display: flex;
}
.login-tool .el-button {
  flex: 1;
}
.to-register {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}
</style>