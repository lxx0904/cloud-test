<!--
 * @Author: lanxx
 * @Date: 2024-02-17 17:33:37
 * @LastEditTime: 2024-02-18 13:44:50
 * @LastEditors: lanxx
 * @Description: Do not edit
 * @FilePath: \vue-hello-world\src\App.vue
-->
<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Welcome to Your Vue.js App" />
</template>

<script>
import cloudbase from "@cloudbase/js-sdk";
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  async created() {
    // 创建实例
    const app = cloudbase.init({
      env: "cloud1-3gq3hc3h2dc32d18",
    });
    const auth = app.auth({
      persistence: "local", // 在显式退出登录之前的 30 天内保留身份验证状态
    });
    if (!auth?.hasLoginState()) {
      localStorage.clear();
      await auth.anonymousAuthProvider().signIn()
    }
    app
      .callFunction({
        name: "test",
        data: {},
      })
      .then((res) => {
        console.log(res);
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
