<template>
  <div class="header">
    <div class="left">
      <img
        src="//lf3-cdn-tos.bytescm.com/obj/static/xitu_juejin_web/e08da34488b114bd4c665ba2fa520a31.svg"
        alt="logo"
        style="height: 30px"
      />
    </div>
    <div class="right">
      <div class="logon" v-if="login">
        <el-avatar>{{ username }}</el-avatar>
      </div>
      <div class="login" v-if="!login">
        <el-link type="primary" href="">登录</el-link>
        <div style="border: 1px solid rgb(199, 199, 199); margin: 0 5px" />
        <el-link type="primary" href="">注册</el-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderComponents",
  data() {
    return {
      login: false,
      username: "",
    };
  },
};
</script>

<style lang="less" scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 49px;
  padding: 10px 15px;
  .right {
    .login {
      display: flex;
    }
  }
}
</style>
