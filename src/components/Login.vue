<template>
  <div class="login_container">
    <div class="login_box">
      <!-- 头像区 -->
      <div class="avatar_box">
        <img src="~@/assets/img/gun.png" alt="avatar" />
      </div>
      <!-- 登录表单 -->
      <div></div>
      <div class="from">
        <el-form
          ref="loginFormRef"
          :model="loginForm"
          :rules="loginFormRules"
          label-width="60px"
          class="login_form"
        >
          <el-form-item prop="username">
            <el-input
              v-model="loginForm.username"
              prefix-icon="iconfont icon-user"
              placeholder="账号"
            ></el-input>
          </el-form-item>
          <el-form-item prop="password">
            <el-input
              v-model="loginForm.password"
              type="password"
              prefix-icon="iconfont icon-3702mima"
              placeholder="密码"
            ></el-input>
          </el-form-item>
          <el-form-item class="btns">
            <el-button type="primary" @click="login">登录</el-button>
            <!-- <el-button type="info" @click="resetLoginForm">重置</el-button> -->
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
/*eslint-disable*/
export default {
  data() {
    return {
      loginForm: {
        username: "admin",
        password: "123456"
      },
      // 表单验证
      loginFormRules: {
        username: [
          { required: true, message: "请输入用户名", trigger: "blur" },
          { min: 2, max: 10, message: "长度在 2 到 10 个字符", trigger: "blur" }
        ],
        password: [
          { required: true, message: "请输入用户密码", trigger: "blur" },
          { min: 6, max: 18, message: "长度在 6 到 18 个字符", trigger: "blur" }
        ]
      }
    };
  },
  methods: {
    // 表单重置按钮
    resetLoginForm() {
      // console.log(this)
      // resetFields：element-ui提供的表单方法
      this.$refs.loginFormRef.resetFields();
    },
    login() {
      // 表单预验证
      // valid：bool类型
      this.$refs.loginFormRef.validate(async valid => {
        // console.log(valid)
        if (!valid) return false;
        // // this.$http.post('login', this.loginForm): 返回值为promise
        // // 返回值为promise，可加await简化操作 相应的也要加async
        // const { data: res } = await this.$http.post("login", this.loginForm);
        // console.log(res)
        // if (res.meta.status !== 200) return this.$message.error("登录失败");
        // this.$message.success("登录成功");
        // // 1、将登陆成功之后的token, 保存到客户端的sessionStorage中; localStorage中是持久化的保存
        // //   1.1 项目中出现了登录之外的其他API接口，必须在登陆之后才能访问
        // //   1.2 token 只应在当前网站打开期间生效，所以将token保存在sessionStorage中
        // window.sessionStorage.setItem("token", res.data.token);





        // let user = {
        //   userName:'admin',
        //   token:'111'
        // }
        // this.$store.commit('login',user)


        // 2、通过编程式导航跳转到后台主页, 路由地址为：/home
        this.$router.push("/home");
      });
    }
  }
};
</script>

<style lang="less" scoped>
/* // lang="less" 支持less格式
// scoped vue的指令，只在当前组件生效 */
.login_container {
  // background-color: #2b4b6b;
  height: 100%;
}
.login_box {
  width: 400px;
  height: 280px;
  background-color: #fff;
  border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  -webkit-transform: translate(-50%, -50%);
  background-color: rgba(0,0,0,0);

  .avatar_box {
    width: 100px;
    height: 100px;
    border: 1px solid #eee;
    border-radius: 50%;
    /* padding: 10px; */
    -webkit-box-shadow: 0 0 10px #ddd;
    /* box-shadow: 0 0 10px #ddd; */
    position: absolute;
    top: -50px;
    left: 50%;
    -webkit-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    background-color: #fff;
    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #eee;
    }
  }
}
.login_form {
  position: absolute;
  bottom: 60px;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}
.btns {
  display: flex;
  justify-content: center;
}
.info {
  font-size: 13px;
  margin: 10px 15px;
}
</style>
<style scope>
.login_container {
  background-image: url("~@/assets/img/login_background.jpg");
  background-size: 100% 100%;
}
.from .btns {
  margin-bottom: 0 !important;
}
/*  样式穿透部分 */
.login_container .el-form-item__content {
  margin-left: 0 !important;
}
.btns .el-form-item__content {
  width: 100%;
}
.btns button {
  width: 100%;
}
</style>