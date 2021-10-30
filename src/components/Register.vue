<template>
  <div class="register-area">
    <div class="top-banner-area">
      <div class="top-banner">
        <img src="../assets/img/register.png">
      </div>
    </div>
    <div class="register-box">
      <el-divider>注册</el-divider>
      <el-form :model="registerDate"
               status-icon
               :rules="rules"
               ref="ruleForm"
               class="demo-ruleForm"
               size="small">
        <el-form-item prop="email">
          <el-input v-model="registerDate.email" placeholder="注册邮箱"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="registerDate.nickname" placeholder="昵称（非必须）"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input type="password"
                    placeholder="密码"
                    v-model="registerDate.password"
                    autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item prop="checkPass">
          <el-input type="password"
                    placeholder="确认密码"
                    v-model="registerDate.checkPass"
                    autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item prop="agreement">
          <el-checkbox-group v-model="registerDate.agreement">
            <el-checkbox name="agreement">
              我已同意
              <router-link to="/protocol">
                <el-link :underline="false">《GeneralProtection网站使用协议》</el-link>
              </router-link>
            </el-checkbox>
          </el-checkbox-group>
        </el-form-item>
        <div class="register-tool">
          <el-button type="primary"
                     @click="submitForm('ruleForm')">注册</el-button>
          <el-button @click="resetForm('ruleForm')">重置</el-button>
        </div>
        <div class="to-login">
          <router-link to="/login">
            <el-link :underline="false">已有账号，直接登录 <i class="el-icon-arrow-right"></i></el-link>
          </router-link>
        </div>
      </el-form>

    </div>
  </div>
</template>

<script>
  export default {
    name: "Register",
    data() {
      var checkEmail = (rule, value, callback) => {
        if (!value) {
          return callback(new Error('注册邮箱不能为空'));
        }
        const emailRegExp = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/;
        if(emailRegExp.test(value)){
          callback();
        }else {
          callback(new Error("邮箱不合法"));
        }
      };
      var validatePass = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('请输入密码'));
        } else {
          if (this.registerDate.checkPass !== '') {
            this.$refs.ruleForm.validateField('checkPass');
          }
          callback();
        }
      };
      var validatePass2 = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('请再次输入密码'));
        } else if (value !== this.registerDate.password) {
          callback(new Error('两次输入密码不一致!'));
        } else {
          callback();
        }
      };
      return {
        registerDate: {
          email: '',
          nickname: '',
          password: '',
          checkPass: '',
          agreement: []
        },
        rules: {
          email: [
            { validator: checkEmail, trigger: 'blur' }
          ],
          password: [
            { validator: validatePass, trigger: 'blur' }
          ],
          checkPass: [
            { validator: validatePass2, trigger: 'blur' }
          ],
          agreement: [
            { type: 'array', required: true, message: '注册前必须同意协议', trigger: 'change' }
          ]
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) { // 通过验证规则，开始注册
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
  }
</script>

<style scoped>
.top-banner-area {
  background: #00a0d8;
  height: 86px;
  text-align: center;
  margin-bottom: 20px;
}
.register-box {
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
.register-tool {
  display: flex;
}
.register-tool .el-button {
   flex: 1;
}
.to-login {
  display: flex;
  justify-content: flex-end;
  margin-top: 10px;
}
</style>