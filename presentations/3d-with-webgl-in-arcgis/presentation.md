
<!-- .slide: data-background="../images/bg-1.png" -->

## 3D with WebGL in ArcGIS

### Samples

<br/>

<p>Philip Mielke, Esri Redlands</p>
<p>Arno Fiva, Esri R&amp;D Center Z&uuml;rich</p>


---

<!-- .slide: data-background="../images/bg-4.png" -->

## goTo

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="scene-view-go-to-button01"></button>
<pre><code class="lang-ts">// target heading = current heading + 30
var newHeading = view.camera.heading + 30;

// go to heading preserves view.center
view.goTo({
    heading: newHeading
});</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="scene-view-go-to-button02"></button>
<pre><code class="lang-ts">// coordinates (lon, lat) of Mount Fuji
var newCenter = [138.729050, 35.360638];

view.goTo({
   center: newCenter,
   zoom: 13
});</code></pre>
</div>

  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/concepts-goTo.html" ></iframe>
  </div>
</div>


---

<!-- .slide: data-background="../images/bg-4.png" -->

## Filtering

<div class="two-columns">
  <div class="left-column">
<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="mesh-filtering-button01"></button>
<pre><code class="lang-js">// only show buildings constructed before 1900
sceneLayer.definitionExpression =
  "CNSTRCT_YR < 1900 AND CNSTRCT_YR > 0";
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="mesh-filtering-button03"></button>
<pre><code class="lang-js">// reset filter
sceneLayer.definitionExpression = null;
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="mesh-filtering-button02"></button>
<pre><code class="lang-js">// only show tall buildings
sceneLayer.definitionExpression =
  "HEIGHTROOF > 300";
</code></pre>
</div>

  </div>
  <div class="right-column">
    <iframe id="scene-layer-mesh2" data-src="./samples/concepts-definitionExpression.html" ></iframe>
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-4.png" -->

## Assigning a renderer

<div class="two-columns">
  <div class="left-column">
<div class="code-snippet" style="font-size: 130%;">
<button class="play" id="mesh-renderer-button01"></button>
<pre><code class="lang-js">// draw buildings in transparent green
sceneLayer.renderer = {
  type: "simple",
  symbol: {
    type: "mesh-3d",
    symbolLayers: [{
      type: "fill",
      material: {
        color: [144, 238, 144, 0.3]
      }
    }]
  }
};
</code></pre>
</div>

<div class="code-snippet" style="font-size: 130%;">
<button class="play" id="mesh-renderer-button02"></button>
<pre><code class="lang-js">// color buildings by construction year
sceneLayer.renderer = {
 type: "simple",
 visualVariables: [{
   type: "color",
   field: "CNSTRCT_YR",
   stops: [{
       value: 1867,
       color: [69, 83, 122]
     },
     ...
   ]
 }]
};
</code></pre>
</div>

  </div>
  <div class="right-column">
    <iframe id="scene-layer-mesh2" data-src="./samples/concepts-renderer.html" ></iframe>
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-4.png" -->

## Underground

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 130%;">
<button class="play" id="showUndergroundButton"></button>
<pre><code class="lang-js">// remove basemap
map.basemap = null;
// assign surface color so we still see the ground
map.ground.surfaceColor = "#AAA";
// set ground opacity to 0.4 to see through it
map.ground.opacity = 0.4;
</code></pre>
</div>

<div class="code-snippet" style="font-size: 130%;">
<button class="play" id="goUndergroundButton"></button>
<pre><code class="lang-js">// remove navigation constraints
map.ground.navigationConstraint = {
  type: "none"
};

// underground camera position
view.goTo(new Camera({
  position: {
    spatialReference: SpatialReference.WebMercator,
    x:-8238933.779779457,
    y:4968874.720108374,
    z:-6.607122800312936
  },
  heading: 11.88045761396725,
  tilt: 105.15918832469535}),
</code></pre>
</div>

  </div>
  <div class="right-column">
    <iframe id="scene-layer-mesh2" data-src="./samples/underground.html" ></iframe>
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-4.png" -->

## BuildingSceneLayer

<div style="font-size: 60%;">
  [Sample on ArcGIS API for JavaScript](https://developers.arcgis.com/javascript/latest/sample-code/building-scene-layer-slice)
</div>

<div class="two-columns">
  <div class="left-column">

<div>Create BuildingSceneLayer</div>
<div class="code-snippet" style="font-size: 120%;margin-top: 20px;">
<pre><code class="lang-js" style="margin-bottom: 20px;">
const buildingLayer = new BuildingSceneLayer({
  url: tileServer + "/Esri_Admin_Building/SceneServer",
  title: "Administration Building"
});
map.layers.add(buildingLayer);
</code></pre></div>

<div>Hide Sublayer</div>
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
