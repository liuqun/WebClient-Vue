# IgsTdtLayer

## Props

All common [layers props](/zh/api/Layers/README.md#props)

### `source`

- **类型:** `Object | String`
- **Non-Synced**
- **描述:** A raster tile source.
- **参考:** `Raster source` in [Mapbox Style Spec](https://docs.mapbox.com/mapbox-gl-js/style-spec/#sources-raster)

### `url`

- **类型:** `String`
- **默认值:** `null`
- **Non-Synced**
- **描述:** 完整的地图请求路径。当 url 不为空时，除了 tileSize，其他参数无效

### `tileSize`

- **类型:** `Number`
- **默认值:** `512`
- **Non-Synced**
- **描述:** 输出瓦片大小。

### `domain`

- **类型:** `String`
- **默认值:** `null`
- **Non-Synced**
- **描述:** igs 服务域名。(domain 和（protocol，ip，port）二选一)
- **示例:** `http://localhost:6163`

### `protocol`

- **类型:** `String`
- **默认值:** `location.protocol.split(":")[0] || "http"`
- **Non-Synced**
- **描述:** igs 服务网络协议。(domain 和（protocol，ip，port）二选一)

### `ip`

- **类型:** `String`
- **默认值:** `localhost`
- **Non-Synced**
- **描述:** igs 服务 ip。(domain 和（protocol，ip，port）二选一)

### `port`

- **类型:** `String`
- **默认值:** `6163`
- **Non-Synced**
- **描述:** igs 服务 port。(domain 和（protocol，ip，port）二选一)

### `layerType`

- **类型:** `String`
- **默认值:** `vec`
- **Non-Synced**
- **描述:** 图层类型。vec：天地图矢量数据；img：天地图影像数据；cva：天地图矢量注记数据；cia：天地图影像注记数据；vec_igs：天地图矢量数据(通过 IGS)；img_igs：天地图影像数据(通过 IGS)；cva_igs：天地图矢量注记数据(通过 IGS)；cia_igs：天地图影像注记数据(通过 IGS)

### `token`

- **类型:** `String`
- **Required**
- **Non-Synced**
- **描述:** 请求天地图的 key 值

### `baseURL`

- **类型:** `String`
- **默认值:** `null`
- **Non-Synced**
- **描述:** 请求的基地址。

### `crs`

- **类型:** `String`
- **默认值:** `EPSG:4326`
- **Non-Synced**
- **描述:** 空间坐标参考系。

### `isLabel`

- **类型:** `Boolean`
- **默认值:** `false`
- **Non-Synced**
- **描述:** 是否为标签图层。

### `version`

- **类型:** `String`
- **默认值:** `1.0.0`
- **Non-Synced**
- **描述:** 请求的版本号，支持 1.0.0 版本

### `tdtStyle`

- **类型:** `String`
- **默认值:** `default`
- **Non-Synced**
- **描述:** 天地图样式

### `format`

- **类型:** `String`
- **默认值:** `tiles`
- **Non-Synced**
- **描述:** 输出格式

## Events

All common layer [events](/zh/api/Layers/#events)

## Example

```vue
<template>
  <mapbox-map
    class="main"
    :accessToken="accessToken"
    :mapStyle="mapStyle"
    :zoom="mapZoom"
    :center="outerCenter"
    :crs="mapCrs"
  >
    <mapbox-igs-tdt-layer
      :layer="layer"
      :layerId="layerId"
      :sourceId="sourceId"
      :baseURL="baseURL"
      :token="token"
      :crs="mapCrs"
    >
    </mapbox-igs-tdt-layer>
  </mapbox-map>
</template>

<script>
import "@mapgis/mapbox-gl/dist/mapbox-gl.css";
import Mapbox from "@mapgis/mapbox-gl";
import { MapboxMap, MapboxIgsTdtLayer } from "@mapgis/webclient-vue-mapboxgl";

export default {
  components: {
    MapboxMap,
    MapboxIgsTdtLayer
  },
  data() {
    return {
      accessToken:
        "pk.eyJ1IjoicGFybmRlZWRsaXQiLCJhIjoiY2o1MjBtYTRuMDhpaTMzbXhpdjd3YzhjdCJ9.sCoubaHF9-nhGTA-sgz0sA", // 使用mapbox样式需要的秘钥
      mapStyle: "mapbox://styles/mapbox/light-v9", // 地图样式
      mapZoom: 3, // 地图初始化级数
      outerCenter: [130, 30], // 地图显示中心
      mapCrs: "EPSG:4326",

      layerId: "igsLayer_layerId",
      sourceId: "igsLayer_sourceId",
      layer: {}, // 图层配置信息
      baseURL: "http://t2.tianditu.gov.cn/vec_c/wmts", // 请求基地址
      token: "2ddaabf906d4b5418aed0078e1657029" // 请求天地图的key值
    };
  },

  created() {
    // 在组件中使用mapbox-gl.js的脚本库功能
    this.mapbox = Mapbox;
  }
};
</script>

<style lang="css">
.main {
  height: 600px;
  width: 100%;
}
</style>
```
