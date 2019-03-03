
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
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-4.png" data-title="feature-filter" -->

## Filter

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="buildings_goto_button"></button>
<pre><code class="lang-ts">view.goTo(buildingLayer);</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="buildings_filter_button"></button>
<pre><code class="lang-ts">var geometry = {
  type: "polygon",
  rings: [
    [-13045144.22519497, 4036815.986120914],
    [-13045149.901010452, 4036915.714135076],
    [-13045241.422037635, 4036939.3821808314],
    [-13045195.95151689, 4036815.973322056]
  ],
  spatialReference: SpatialReference.WebMercator,
};

layerView.filter = new FeatureFilter({
  geometry: geometry,
});</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="addBSLButton"></button>
<pre><code class="lang-ts">adminBuildingLayer.visible = true;</code></pre>
</div>

  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>


---

<!-- .slide: data-background="../images/bg-4.png" data-title="building-scene-layer-widgets" -->

## Building Scene Layer

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="startLineMeasureButton"></button>
<pre>
<code class="lang-ts">new DirectLineMeasurement3D({
  view: view
}).viewModel.newMeasurement();</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="startAreaMeasureButton"></button>
<pre><code class="lang-ts">var widget = new AreaMeasurement3D({
  view: view
});
widget.viewModel.newMeasurement();</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="startSliceButton"></button>
<pre><code class="lang-ts">var widget = new Slice({
  view: view
});
widget.viewModel.newSlice();

// exclude layers from slice
widget.viewModel.excludedLayers
  .addMany(structuralSublayers);</code></pre>
</div>


  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>




---

<!-- .slide: data-background="../images/bg-4.png" data-title="building-scene-layer-api" -->

## Building Scene Layer

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="hideWallsButton"></button>
<pre><code class="lang-ts">Hide walls</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="hideRoofButton"></button>
<pre><code class="lang-ts">Hide roof</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="hideWindowsButton"></button>
<pre><code class="lang-ts">Hide windows</code></pre>
</div>


  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>


---

<!-- .slide: data-background="../images/bg-4.png" data-title="underground" -->

## Underground

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="showUndergroundButton"></button>
<pre>
<code class="lang-ts">
sewerLayer.visible = true;
adminBuildingLayer.opacity = 0.4;
webscene.ground.opacity = 0.4;
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="goUndergroundButton"></button>
<pre>
<code class="lang-ts">
webscene.ground.navigationConstraint = {
  type: "none",
};
view.goTo(undergroundCamera);</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="goWaterNetworkButton"></button>
<pre>
<code class="lang-ts">
webscene.ground.navigationConstraint = {
  type: "none",
};
view.goTo(undergroundCamera);</code></pre>
</div>

  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>


---

<!-- .slide: data-background="../images/bg-4.png" data-title="rendering-environment" -->

## Rendering

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="showCampusButton"></button>
<pre>
<code class="lang-ts">
view.goTo(campusCamera, { duration: 5000 });
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="highQualityButton"></button>
<pre>
<code class="lang-ts">
view.lighting.ambientOcclusionEnabled = true;
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="sunsetButton"></button>
<pre>
<code class="lang-ts">
// Sunset
</code></pre>
</div>


  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>


---

<!-- .slide: data-background="../images/bg-4.png" data-title="rendering-nightmode" -->

## Rendering

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="showTacticalViewButton"></button>
<pre>
<code class="lang-ts">view.goTo(tacticalCamera);
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="darkBuildingsButton"></button>
<pre>
<code class="lang-ts">
buildingLayer = darkBuildingRenderer;
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="darkBasemapButton"></button>
<pre>
<code class="lang-ts">
view.basemap = "";
</code></pre>
</div>


  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>


---

<!-- .slide: data-background="../images/bg-4.png" data-title="rendering-dispatch" -->

## Rendering

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="showTacticalTeamsButton"></button>
<pre>
<code class="lang-ts">view.goTo(tacticalCamera);
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="showLocationButton"></button>
<pre>
<code class="lang-ts">
buildingLayer = darkBuildingRenderer;
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="trackLocationButton"></button>
<pre>
<code class="lang-ts">
view.basemap = "";
</code></pre>
</div>


  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>
