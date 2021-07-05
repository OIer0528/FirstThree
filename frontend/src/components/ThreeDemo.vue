<template>
  <div id="three" style="height: 500px; width: 500px"></div>
</template>

<script>
import * as THREE from "three";
export default {
  name: "ThreeDemo",
  props: ["animationSpeed"],
  computed: {
    speed: function () {
      return this.animationSpeed / 2000;
    },
  },
  mounted() {
    this.playAnimation();
  },
  methods: {
    playAnimation() {
      // 获取绘图区域
      const el = document.getElementById("three");
      const ratio = el.clientWidth / el.clientHeight;

      // 创建渲染器
      let render = new THREE.WebGL1Renderer();
      render.setClearColor("#c0c0c0");
      render.setSize(el.clientWidth, el.clientHeight);
      el.appendChild(render.domElement);

      // 创建场景和几何体
      let scene = new THREE.Scene();
      let geometry = new THREE.BoxGeometry(2, 2, 2);
      let material = new THREE.MeshPhongMaterial({ color: 0x00ff00 });
      let cube = new THREE.Mesh(geometry, material);
      scene.add(cube);

      // 创建相机
      let camera = new THREE.PerspectiveCamera(45, ratio, 0.1, 1000);
      camera.position.set(1, 1, 10);
      camera.up.set(0, 1, 0);
      camera.lookAt(new THREE.Vector3(0, 0, 0));

      // 光源
      let light = new THREE.DirectionalLight(0xffff00);
      light.position.set(10, 10, 10);
      scene.add(light);

      // 渲染函数
      let renderFunc = function () {
        requestAnimationFrame(renderFunc);
        cube.rotation.x += this.speed; //动起来
        cube.rotation.y += this.speed; //动起来
        render.render(scene, camera);
      }.bind(this);
      renderFunc();
    },
  },
};
</script>

<style scoped>
#three {
  border: solid black 3px;
}
</style>