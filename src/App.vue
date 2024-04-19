<script setup>
import { ref, reactive, onMounted } from 'vue'
import { Ion, Viewer, Camera, Rectangle } from 'cesium'
import "cesium/Build/Cesium/Widgets/widgets.css";

// 存放workers,thirdParty,assets,widgets四个目录的位置 -- 要配置的否则加载不到相应资源
window.CESIUM_BASE_URL = "/"
// 设置cesium token
Ion.defaultAccessToken = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJhMzZlNDQzZi03ZDM2LTRmMTAtODU2NC02ZDE0ZTdmOTZhNWMiLCJpZCI6MTk5OTk4LCJpYXQiOjE3MDk3MTM0Mzd9.-SiToEtm1T5RtE8wH6NMJo8bMplIwU-nZ4p6ddD0OzE"
// 设置cesium默认视角
Camera.DEFAULT_VIEW_RECTANGLE = Rectangle.fromDegrees(
  // 西经
  73.33,
  // 南纬
  53.33,
  // 东经
  135,
  // 北纬
  3.51
)

onMounted(() => {
  const viewer = new Viewer('cesiumContainer', {
    // creditContainer: "cesiumContainer" // 通过此配置，可以隐藏logo，属性值为要隐藏logo的cesium容器
    // infoBox: false, // 信息框控制台会报错，设置为false则不会再报错了
  })

  // 也可以通过js的方式隐藏logo
  viewer.cesiumWidget.creditContainer.style.display = "none"
})

</script>

<template>
  <!-- cesium容器 -->
  <div id="cesiumContainer" ref="cesiumContainer"></div>
</template>

<style lang='scss' scoped>
* {
  margin: 0;
  padding: 0;
}

#cesiumContainer {
  width: 100vw;
  height: 100vh;
}
</style>