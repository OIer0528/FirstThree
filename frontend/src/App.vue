<template>
  <div>
    <el-container>
      <el-header>
        <h1>第一个 Three.js 示例项目</h1>
      </el-header>
      <el-main>
          <el-row>
            <el-col :xs="{span:24,offset:0}" :sm="{span:16,offset:4}" :md="{span:12,offset:6}">
              <ThreeDemo />
            </el-col>
          </el-row>
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

#app .el-footer {
  background: rgb(179, 216, 255);
  position: fixed;
  width: 100%;
  bottom: 0;
}
</style>
