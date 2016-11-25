<template>

<div>
  <div class="logo container">
    <img src="../assets/logo.jpg">
  </div>
  <div class="login container">
    <el-form :model="ruleForm2" :rules="rules2" ref="ruleForm2" label-position="left" label-width="0px" class="demo-ruleForm card-box loginform">
      <h3 class="title">用户登录</h3>
      <el-form-item prop="account">
        <el-input type="text" v-model="ruleForm2.account" auto-complete="off" placeholder="账号"></el-input>
      </el-form-item>
      <el-form-item prop="checkPass">
        <el-input type="password" v-model="ruleForm2.checkPass" auto-complete="off" placeholder="密码"></el-input>
      </el-form-item>
      <el-form-item prop="auth" style="line-height:0">
        <el-col :span="12">
          <el-input type="text" v-model="ruleForm2.auth" auto-complete="off" placeholder="验证码"></el-input>
        </el-col>
        <el-col :span="10" :offset="1">
          <img src="../assets/author.png" style="height:36px;">
        </el-col>
      </el-form-item>
      <el-form-item style="width:100%;">
        <el-button type="primary" style="width:100%;" @click.native.prevent="handleSubmit2">登录</el-button>
        <!--<el-button @click.native.prevent="handleReset2">重置</el-button>-->
      </el-form-item>
    </el-form>
  </div>
  <div class="bottom container">版权所有：Copyright © 2016 英泰伟业科技（北京）有限公司</div>
</div>
</template>

<script>
  export default {
    data() {
      return {
        ruleForm2: {
          account: '',
          checkPass: ''
        },
        rules2: {
          account: [
            { required: true, message: '请输入账号', trigger: 'blur' },
            //{ validator: validaePass }
          ],
          checkPass: [
            { required: true, message: '请输入密码', trigger: 'blur' },
            //{ validator: validaePass2 }
          ]
        },
        checked: true
      };
    },
    methods: {
      handleReset2() {
        this.$refs.ruleForm2.resetFields();
      },
      handleSubmit2(ev) {
        var _this=this;
        this.$refs.ruleForm2.validate((valid) => {
          if (valid) {
            //_this.$router.push('/table');
            _this.$router.replace('/table');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      }
    }
  }
</script>

<style scoped>
  .container { margin:0 auto; }
  .logo { margin-top:70px; width:1024px; }
  .login{ width:486px;height:416px;padding:42px 0 0 538px;background:url(../assets/login-bj.jpg) no-repeat; }
  .bottom{ width:1024px;height:46px;line-height:46px;font-size:12px;color:#fff;text-align:center;background:#bc1b21;margin-top:14px;}
  .login .card-box {
    padding: 30px;
    -webkit-border-radius: 5px;
    border-radius: 5px;
    -moz-border-radius: 5px;
    background-clip: padding-box;
    margin-bottom: 20px;
    background-color: #fff;
    width: 270px;
  }

  .title {
    margin: 0px auto 40px auto;
    text-align: center;
    color: #505458;
  }

  .loginform {
    width: 350px;
    padding: 35px 35px 15px 35px;
  }
</style>
