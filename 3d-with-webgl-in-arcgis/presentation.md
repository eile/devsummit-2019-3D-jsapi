
<!-- .slide: data-background="../images/bg-1.png" -->

## 3D with WebGL in ArcGIS

### Samples

<br/>

<p>Philip Mielke, Esri Redlands</p>
<p>Arno Fiva, Esri R&amp;D Center Z&uuml;rich</p>


---

<!-- .slide: data-background="../images/bg-4.png" data-title="feature-filter" -->

## goTo

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="addBasemapButton"></button>
<pre><code class="lang-ts">// Show basemap 2D and tilt</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="addElevationButton"></button>
<pre><code class="lang-ts">// Add mountains</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="addBuildingsButton"></button>
<pre><code class="lang-ts">// Add building scene layer, lights, trees
var sceneLayer = new SceneLayer({
  url: ".../Buildings_TODO/SceneServer",
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
<pre><code class="lang-ts">// Define polygon vertices
var polygon = new Polygon({
  rings: [
    [-13045144.22519497, 4036815.986120914],
    [-13045149.901010452, 4036915.714135076],
    ...
  ],
});</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="gotoBuildingButton"></button>
<pre><code class="lang-ts">// Zoom to building
view.goTo(polygon).then(function() {
  // Draw polygon
  view.graphics.add(new Graphic({
    symbol: { type: "fill", color: "orange" },
    geometry: polygon,
  }));
});</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="buildings_filter_button"></button>
<pre><code class="lang-ts">// Filter buildings inside polygon
layerView.filter = new FeatureFilter({
  geometry: geometry,
  spatialRelationship: "disjoint",
});</code></pre>
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
<button class="play" id="addBSLButton"></button>
<pre><code class="lang-ts">TODO</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<pre><code class="lang-ts">// Retrieve building sublayer
function getSublayer(title) {
  adminBuildingLayer.allSublayers.find(
    function(sublayer) {
      return sublayer.title === title;
});}</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="hideWallsButton"></button>
<pre><code class="lang-ts">// Hide sublayer named "Walls"
getSublayer("Walls").visible = false;</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="hideRoofButton"></button>
<pre><code class="lang-ts">// Hide roof and windows
getSublayer("Roof").visible = false;
getSublayer("Windows").visible = false;</code></pre>
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
widget.viewModel.excludedLayers.addMany(
    getSublayer("Floors"),
    getSublayer("Structural"),
    getSublayer("Furniture"), ...);</code></pre>
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
<code class="lang-ts">// Add underground features
TODO
// Make ground transparent
adminBuildingLayer.opacity = 0.4;
webscene.ground.opacity = 0.4;
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="goUndergroundButton"></button>
<pre>
<code class="lang-ts">// Remove navigation constraints
webscene.ground.navigationConstraint = {
  type: "none"
};

// Place camera underground
view.goTo(undergroundCamera);</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="goWaterNetworkButton"></button>
<pre>
<code class="lang-ts">// Show closeup of sewer system
view.goTo(sewerCamera);</code></pre>
</div>

  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>


---

<!-- .slide: data-background="../images/bg-4.png" data-title="rendering-environment" -->

## Rendering: Quality & Lighting

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="highQualityButton"></button>
<pre>
<code class="lang-ts">// Atmosphere settings
view.environment.starsEnabled = true;
view.environment.atmosphereEnabled = true;
view.environment.atmosphere = {
  quality: "high"
};
// Lighting settings
view.environment.lighting = {
  date: "Thu Mar 15 2018 16:30:00 PST",
  directShadowsEnabled: true,
  ambientOcclusionEnabled: true,
  cameraTrackingEnabled: false,
};
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="sunsetButton"></button>
<pre>
<code class="lang-ts">// Animated sunset
Slide.createFrom(view).then(function(slide) {
  slide.view.environment.lighting.date =
    "Thu Mar 15 2018 19:30:00 PST";
  slide.applyTo(view, { duration: 15000 });
});
</code></pre>
</div>


  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>


---

<!-- .slide: data-background="../images/bg-4.png" data-title="rendering-nightmode" -->

## Rendering: Colors & Basemaps

<div class="two-columns">
  <div class="left-column">

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="showTacticalViewButton"></button>
<pre>
<code class="lang-ts">view.goTo(esriCampusCamera);
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="darkBuildingsButton"></button>
<pre>
<code class="lang-ts">// Buildings with white edges
buildingLayer.renderer = {
  symbol: TODO...
};
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="darkBasemapButton"></button>
<pre>
<code class="lang-ts">// Apply color scheme to vector tile layer
vectorTileLayer.styling = TODO;

</code></pre>
</div>


  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>


---

<!-- .slide: data-background="../images/bg-4.png" data-title="rendering-dispatch" -->

## Location

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
<code class="lang-ts">// Add location tracking widget
var track = new Track({
  view: view,
});
track.start();
</code></pre>
</div>

<div class="code-snippet" style="font-size: 160%;">
<button class="play" id="trackLocationButton"></button>
<pre>
<code class="lang-ts">// Called when location updates
track.on("track", function() {
  // Point camera to new location
  var location = track.graphic.geometry;
  view.goTo({
    center: location,
    tilt: 60,
    scale: 1200,
  });
});
</code></pre>
</div>


  </div>
  <div class="right-column">
    <iframe id="go-to-demo" data-src="./samples/redlands.html" ></iframe>
  </div>
</div>
