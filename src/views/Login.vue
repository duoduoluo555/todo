<template>
  <div class="login-container">
    <h2 class="login-title">Todo 登录页面</h2>
    <a-form ref="form" :model="form" class="login-form">
      <h2 class="title">用户登录 LOGIN</h2>
      <a-form-item>
        <a-input v-model="form.username">
          <a-icon slot="prefix" type="user"></a-icon>
        </a-input>
      </a-form-item>
      <a-form-item>
        <a-input-password v-model="form.password">
          <a-icon slot="prefix" type="unlock"></a-icon>
        </a-input-password>
      </a-form-item>
      <a-form-item>
        <a-button class="submit" type="primary" @click="login">登录</a-button>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        username: "admin",
        password: "admin",
      },
    };
  },
  methods: {
    login() {
      console.log("登陆成功！");
      this.$router.push("/todo");
    },
  },
};
</script>
<style scoped lang="less">
.login-form {
  width: 565px;
  height: 372px;
  margin: 0 auto;
  padding: 40px 110px;
  background: url('../assets/input.png');
  background-repeat: no-repeat;
}

/* 背景 */
.login-container {
  position: absolute;
  width: 100%;
  height: 100%;
  background: url('../assets/bg.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

/* Log */
.login-title {
  margin: 100px 0 60px;
  color: #fff;
  font-size: 36px;
  font-family: Microsoft Yahei;
  text-align: center;
}

/* 登陆按钮 */
.submit {
  width: 100%;
  height: 45px;
  font-size: 16px;
}

/* 用户登陆标题 */
.title {
  margin-bottom: 50px;
  color: #fff;
  font-weight: 700;
  font-size: 24px;
  font-family: Microsoft Yahei;
}

/* 输入框内左边距50px */
.ant-input-affix-wrapper .ant-input:not(:first-child) {
  padding-left: 50px;
}
</style>
