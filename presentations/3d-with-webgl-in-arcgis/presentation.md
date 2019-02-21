
<!-- .slide: data-background="../images/bg-1.png" -->

## 3D with WebGL in ArcGIS

### Samples

<br/>

<p>Philip Mielke, Esri Redlands</p>
<p>Arno Fiva, Esri R&amp;D Center Z&uuml;rich</p>

---

<!-- .slide: data-background="../images/bg-4.png" -->

## BuildingSceneLayer

<div style="font-size: 60%;">
  [Sample on ArcGIS API for JavaScript](https://developers.arcgis.com/javascript/latest/sample-code/building-scene-layer-slice)
</div>

<div class="two-columns">
  <div class="left-column">

<div>Create BuildingSceneLayer:</div>
<div class="code-snippet" style="font-size: 120%;margin-top: 20px;">
<pre><code class="lang-js" style="margin-bottom: 20px;">
const buildingLayer = new BuildingSceneLayer({
  url: tileServer + "/Esri_Admin_Building/SceneServer",
  title: "Administration Building"
});
map.layers.add(buildingLayer);
</code></pre></div>

<div>Hide sublayer:</div>
<div class="code-snippet" style="font-size: 120%;margin-top: 20px;">
<button class="play" id="hideLayerButton"></button>
<pre><code class="lang-js" style="margin-bottom: 20px;">
buildingLayer.allSublayers.forEach(function(layer) {
  if (layer.modelName === "Overview") {
    layer.visible = !layer.visible;
  }
});
</code></pre></div>

  </div>
  <div class="right-column">
    <iframe id="scene-view-map-view" data-src="./samples/building-scene-layer.html"></iframe>
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-4.png" -->

## 3D Measurements

<div style="font-size: 60%;">
  [Sample on ArcGIS API for JavaScript](https://developers.arcgis.com/javascript/latest/sample-code/widgets-measurement-3d)
</div>

<div class="two-columns">
  <div class="left-column">

<div>Line Measurements</div>
<div class="code-snippet" style="font-size: 140%;margin-top: 20px;">
<pre><code class="lang-js" style="margin-bottom: 20px;">
var widget = new DirectLineMeasurement3D({
  view: view
});

widget.viewModel.newMeasurement();

view.ui.add(widget, "bottom-right");
</code></pre></div>

  </div>
  <div class="right-column">
    <iframe id="scene-view-map-view" data-src="./samples/3d-measurements.html"></iframe>
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-4.png" -->

## Point Styles

<div style="font-size: 60%;">
  [Sample on ArcGIS API for JavaScript](https://developers.arcgis.com/javascript/latest/sample-code/visualization-point-styles)
</div>

<div class="two-columns">
  <div class="left-column">

<div>Add Callouts</div>
<div class="code-snippet" style="font-size: 120%;margin-top: 20px;">
<button class="play" id="addPointsLayerButton"></button>
<pre><code class="lang-js" style="margin-bottom: 20px;">
var pointsLayer = new FeatureLayer({
  url: server + "/LyonPointsOfInterest/FeatureServer"
  title: "Touristic attractions",
  elevationInfo: { mode: "relative-to-scene" },
  renderer: pointsRenderer,
  ...
}
map.layers.add(pointsLayer);
</code></pre></div>  

<div>Declutter</div>
<div class="code-snippet" style="font-size: 120%;margin-top: 20px;">
<button class="play" id="declutterButton"></button>
<pre><code class="lang-js" style="margin-bottom: 20px;">
pointsLayer.featureReduction = {
  type: "selection"
};
</code></pre></div>

<div>Improve Perspective</div>
<div class="code-snippet" style="font-size: 120%;margin-top: 20px;">
<button class="play" id="improvePerspectiveButton"></button>
<pre><code class="lang-js" style="margin-bottom: 20px;">
pointsLayer.screenSizePerspectiveEnabled = true;
</code></pre></div>

  </div>
  <div class="right-column">
    <iframe id="scene-view-map-view" data-src="./samples/visualization-point-styles.html"></iframe>
  </div>
</div>
