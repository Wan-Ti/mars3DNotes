## 自定义tooltips样式

```
    bindLayerTooltip(layer) {
      layer.bindTooltip(
        (event) => {
          if (event.graphic.cluster && event.graphic.getGraphics) {
            const graphics = event.graphic.getGraphics(); // 对应的grpahic数组，可以自定义显示
            if (graphics) {
              this.showPop = false;
              return;
            }
          } else {
            this.popInfo.popColumnLit = [];
            this.mapObj = event.graphic.attr;
            let targetHtml = document.querySelector("#mapPop").innerHTML;
            return targetHtml;
          }
        },
        {
          className: "mapPop",
          hasCache: true,
          timeRender: true,
          scaleByDistance: true,
          scaleByDistance_far: 50000,
          scaleByDistance_farValue: 0.6,
          distanceDisplayConditionl: true,
          distanceDisplayCondition_far: 2000,
          clampToGround: true,
          direction: "top",
          enterable: true,
        }
      );
    },
```

## 地图添加地名等注记图层

```
const titleLayer = new mars3d.layer.TdtLayer({
  name: "注记",
  type: "tdt",
  layer: "img_z",
  crs: "EPSG:4326",
  zIndex: 99999,
  key: mars3d.Token.tiandituArr,
});
this.mars3dContainer.addLayer(titleLayer);        
```

## 根据ID控制图层显隐

```
    operateTargetLayer(id, type) {
      let layer = this.mars3dContainer.getLayerById(id);
      if (layer) {
        switch (type) {
          case "remove":
            this.mars3dContainer.removeLayer(layer);
            break;
          case "hide":
            layer.show = false;
            break;
          case "show":
            layer.show = true;
            break;
        }
      }
    },
```  
