<script setup>
import { ref, reactive, onMounted } from 'vue'
import * as Cesium from 'cesium'
import "cesium/Build/Cesium/Widgets/widgets.css";

// 存放workers,thirdParty,assets,widgets四个目录的位置 -- 要配置的否则加载不到相应资源
window.CESIUM_BASE_URL = "/"

onMounted(() => {
  const viewer = new Cesium.Viewer('cesiumContainer')
})

</script>

<template>
  <!-- cesium容器 -->
  <div id="cesiumContainer" ref="cesiumContainer"></div>
</template>

<style lang='scss' scoped>
 *{
  margin: 0;
  padding: 0;
 }
 #cesiumContainer{
  width: 100vw;
  height: 100vh;
 }
</style>