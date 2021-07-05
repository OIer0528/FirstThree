<template>
  <div>
    <el-container>
      <el-header>
        <h1>第一个 Three.js 示例项目</h1>
      </el-header>
      <el-main>
        <div class="DemoArea">
          <ThreeDemo v-bind:animationSpeed="animationSpeed" />
        </div>
        <div class="SettingArea">
          <span>动画速度：{{ animationSpeed }}</span>
          <el-slider v-model="animationSpeed"></el-slider>
        </div>
      </el-main>
      <el-footer> <Footer /> </el-footer>
    </el-container>
  </div>
</template>

<script>
import Footer from "./components/Footer.vue";
import ThreeDemo from "./components/ThreeDemo.vue";

export default {
  name: "App",
  components: {
    Footer,
    ThreeDemo,
  },
  data() {
    return { animationSpeed: 20 };
  },
};
</script>

<style>
body {
  margin: 0px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

#app .el-header {
  background: rgb(83, 168, 255);
  color: #ffffff;
}

#app .el-main .DemoArea {
  display: flex;
  justify-content: space-evenly;
  padding-top: 20px;
  padding-bottom: 20px;
}

#app .el-main .SettingArea {
  display: flex;
  justify-content: space-evenly;
  width: 500px;
  margin: 0 auto;
}

#app .el-main .SettingArea .el-slider {
  width: 300px;
}


#app .el-footer {
  background: rgb(179, 216, 255);
  position: fixed;
  width: 100%;
  bottom: 0;
}
</style>
