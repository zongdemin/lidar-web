<template>
  <div id="cesiumContainer">
  </div>
</template>

<script>
import * as Cesium from 'cesium/Source/Cesium.js'
import 'cesium/Build/Cesium/Widgets/widgets.css'
export default {
  name: '',
  mounted () {
   Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI3OTFiOTBiZC0zOGQwLTQyZmItYjFlNy0xMTgxZGE4OGZmNjkiLCJpZCI6NDYyNjksImlhdCI6MTYxNTk5MDQwM30.Gn73KKubCqQT2ONhNGUb3iHnom9nHMqorMTvRC6z7hI'
   Cesium.Viewer('cesiumContainer')
    // 谷歌影像
    // viewer._cesiumWidget._creditContainer.style.display = 'none'
    // var googleImagery = new Cesium.UrlTemplateImageryProvider({
    //   url: 'http://mt{s}.google.cn/vt/lyrs=s&hl=zh-CN&gl=CN&src=app&x={x}&y={y}&z={z}',
    //   subdomains: '0123'
    // })
    // viewer.dataSources.removeAll()
    // viewer.imageryLayers.addImageryProvider(googleImagery)
  }
}
</script>
<style lang="less" scoped>
</style>
