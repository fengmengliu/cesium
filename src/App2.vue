<script setup>
// import { RouterLink, RouterView } from 'vue-router'
// import HelloWorld from './components/HelloWorld.vue'
import * as Cesium from 'cesium'
import "./Widgets/widgets.css"
import { onMounted } from 'vue'

// 设置cesium静态资源的路径 --- 就是那四个文件夹存放的位置
window.CESIUM_BASE_URL = "/"
// 设置cesium默认视角（默认是美国的）  ---  修改为青藏高原
Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(
  89.5, // 西边的经度
  20.4, // 南边的维度
  110.4, // 东边的经度
  61.2 // 北边的维度
)

// 设置cesium token
Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJhMzZlNDQzZi03ZDM2LTRmMTAtODU2NC02ZDE0ZTdmOTZhNWMiLCJpZCI6MTk5OTk4LCJpYXQiOjE3MDk3MTM0Mzd9.-SiToEtm1T5RtE8wH6NMJo8bMplIwU-nZ4p6ddD0OzE'

onMounted(() => {
  let viewer = new Cesium.Viewer("cesiumContainer", {
    infoBox: false, //去掉控制台中，信息框的报错显示
    geocoder: false, //是否展示搜索框
    homeButton: false, // 不显示home按钮
    sceneModePicker: false, //场景查看器
    baseLayerPicker: false, // 是否显示图层选择器
    navigationHelpButton: false, // 是否显示帮助按钮
    // animation: false, // 是否播放动画
    timeline: false, // 是否显示时间轴
    fullscreenButton: false, // 是否显示全屏按钮
    skyBox: new Cesium.SkyBox({ // 设置天空背景
      sources: {
        positiveX: './texture/sky/px.jpg',
        negativeX: './texture/sky/nx.jpg',
        positiveY: './texture/sky/ny.jpg',
        negativeY: './texture/sky/py.jpg',
        positiveZ: './texture/sky/pz.jpg',
        negativeZ: './texture/sky/nz.jpg'
      }
    }),
    // baseLayer: new Cesium.ImageryLayer(new Cesium.WebMapTileServiceImageryProvider({
    //   // url: "http://t0.tianditu.gov.cn/vec_w/wmts?tk=61108e01d62f15f0a8c49614ef6aa217",
    //   url: "http://t0.tianditu.com/vec_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=vec&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=61108e01d62f15f0a8c49614ef6aa217",
    //   layer: "tdtBasicLayer",
    //   style: "default",
    //   format: "image/jpeg",
    //   tileMatrixSetID: "GoogleMapsCompatible"
    // })),
    // 天地图矢量路径图
    // imageryProvider: new Cesium.WebMapTileServiceImageryProvider({
    //   url: "http://t0.tianditu.gov.cn/vec_w/wmts?tk=61108e01d62f15f0a8c49614ef6aa217",
    //   // url: "http://t0.tianditu.com/vec_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=vec&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=61108e01d62f15f0a8c49614ef6aa217",
    //   layer: "tdtBasicLayer",
    //   style: "default",
    //   format: "image/jpeg",
    //   tileMatrixSetID: "GoogleMapsCompatible"
    // })
  })
  // 隐藏左下角logo
  viewer.cesiumWidget.creditContainer.style.display = "none"

  // 天地图
  // const shadedRelief1 = new Cesium.WebMapTileServiceImageryProvider({
  //     url : 'http://t0.tianditu.com/vec_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=vec&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=61108e01d62f15f0a8c49614ef6aa217',
  //     layer: "tdtBasicLayer",
  //     style: "default",
  //     format: "image/jpeg",
  //     tileMatrixSetID: "default028mm"
  //   });
  // 高德地图
  const shadedRelief1 = new Cesium.WebMapTileServiceImageryProvider({
      // url : 'http://t0.tianditu.com/vec_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=vec&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=61108e01d62f15f0a8c49614ef6aa217',
      // layer: "tdtBasicLayer",
      // style: "default",
      // format: "image/jpeg",
      // tileMatrixSetID: "default028mm"
      url: "http://webrd02.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=8&x={x}&y={y}&z={z}",
      layer: "tdtVecBasicLayer",
      style: "default",
      format: "image/png",
      tileMatrixSetID: "GoogleMapsCompatible",
    });
  viewer.imageryLayers.addImageryProvider(shadedRelief1);
})
</script>

<template>
  <div id="cesiumContainer"></div>
  <!-- <header>
    <img alt="Vue lo go" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header> 

  <RouterView /> -->
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

#cesiumContainer {
  width: 100vw;
  height: 100vh;
}
</style>
