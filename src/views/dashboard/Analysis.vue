<template>
  <div class="map-box">
    <div id="cesiumContainer"></div>
  </div>
</template>

<script>
import * as Cesium from 'cesium/Source/Cesium.js'
export default {
  name: '',
  mounted () {
   Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI3OTFiOTBiZC0zOGQwLTQyZmItYjFlNy0xMTgxZGE4OGZmNjkiLCJpZCI6NDYyNjksImlhdCI6MTYxNTk5MDQwM30.Gn73KKubCqQT2ONhNGUb3iHnom9nHMqorMTvRC6z7hI'
   var viewer = Cesium.Viewer('cesiumContainer', {
            geocoder: true,
            sceneModePicker: true,
            navigationHelpButton: true,
            baseLayerPicker: true,
            homeButton: true,
            fullscreenButton: true,
            timeline: true,
            animation: true })
    // 谷歌影像
    viewer._cesiumWidget._creditContainer.style.display = 'none'
    var googleImagery = new Cesium.UrlTemplateImageryProvider({
      url: 'http://mt{s}.google.cn/vt/lyrs=s&hl=zh-CN&gl=CN&src=app&x={x}&y={y}&z={z}',
      subdomains: '0123'
    })
    viewer.imageryLayers.addImageryProvider(googleImagery)
  }
}
</script>
<style scoped>
.map-box {
  width: 1024px;
  height: 768px;
}
#cesiumContainer {
  width: 100%;
  height: 100%;
}
</style>
