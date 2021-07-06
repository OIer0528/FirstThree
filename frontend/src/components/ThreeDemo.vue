<template>
  <div id="three"></div>
</template>

<script>
import * as THREE from "three";
export default {
  name: "ThreeDemo",
  data() {
    return {
      watchTimer: false,
      clientWidth: 0.0,
      clientHeight: 0.0,
      render: undefined,
      camera: undefined,
      speed: 0.01,
    };
  },
  watch: {
    clientWidth(val) {
      if (!this.watchTimer) {
        this.clientWidth = val;
        this.watchTimer = true;
        const that = this;
        setTimeout(function () {
          that.watchTimer = false;
          that.render.setSize(that.clientWidth, that.clientHeight);
          that.camera.aspect = that.clientWidth / that.clientHeight;
          that.camera.updateProjectionMatrix();
        }, 50);
      }
    },
  },
  mounted() {
    // 获得绘图区域
    const el = document.getElementById("three");
    this.clientWidth = el.clientWidth;
    this.clientHeight = el.clientHeight;

    // 侦听窗口大小
    const that = this;
    window.onresize = function () {
      return (() => {
        that.clientWidth = el.clientWidth;
        that.clientHeight = el.clientHeight;
      })();
    };

    // 创建渲染器
    this.render = new THREE.WebGL1Renderer();
    this.render.setClearColor("#c0c0c0");
    this.render.setSize(this.clientWidth, this.clientHeight);
    el.appendChild(this.render.domElement);

    // 添加点击事件
    this.render.domElement.addEventListener("touchstart", (e) => {
      e.stopPropagation();
      that.speed = 0.0;
    });
    this.render.domElement.addEventListener("touchend", () => {
      that.speed = 0.01;
    });

    // 创建相机
    const ratio = this.clientWidth / this.clientHeight;
    this.camera = new THREE.PerspectiveCamera(45, ratio, 0.1, 1000);
    this.camera.position.set(1, 1, 10);
    this.camera.up.set(0, 1, 0);
    this.camera.lookAt(new THREE.Vector3(0, 0, 0));

    this.playAnimation();
  },
  methods: {
    playAnimation() {
      // 创建场景和几何体
      let scene = new THREE.Scene();
      let geometry = new THREE.BoxGeometry(2, 2, 2);
      let material = new THREE.MeshPhongMaterial({ color: 0x00ff00 });
      let cube = new THREE.Mesh(geometry, material);
      scene.add(cube);

      // 光源
      let light = new THREE.DirectionalLight(0xffff00);
      light.position.set(10, 10, 10);
      scene.add(light);

      // 渲染函数
      let renderFunc = function () {
        requestAnimationFrame(renderFunc);
        cube.rotation.x += this.speed; //动起来
        cube.rotation.y += this.speed; //动起来
        this.render.render(scene, this.camera);
      }.bind(this);
      renderFunc();
    },
  },
};
</script>

<style scoped>
#three {
  border: solid black 3px;
  width: 100%;
  height: 500px;
}
</style>