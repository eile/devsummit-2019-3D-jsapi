
<!-- .slide: data-background="images/bg-1.png" -->

### Interactive 3D Maps with the<br/> ArcGIS API for JavaScript

### _Getting Started_
<p style="font-size: 75%"><br/>
  Johannes Schmid, Esri R&amp;D Center Z&uuml;rich<br/>
  Arno Fiva, Esri R&amp;D Center Z&uuml;rich
</p>
<p><br/><small>
Live version of this presentation:<br>https://arcgis.github.io/devsummit-2019-3D-jsapi/presentations/3d-maps-with-the-arcgis-js-api-getting-started
</small></p>

---

<!-- .slide: data-background="images/bg-4.png" -->

## Fancy example

<i>This is what you will learn to do</i>

---

<!-- .slide: data-background="images/bg-2.png" -->

## Preface

- This session is about writing JavaScript & HTML!
- Esri provides configurable applications
  - [SceneViewer](https://www.esri.com/en-us/arcgis/products/3d-scene-viewer)
  - [Story Maps](https://storymaps.arcgis.com/en/)
  - [Web AppBuilder](https://www.esri.com/en-us/arcgis/products/web-appbuilder/overview)
  
---

<!-- .slide: data-background="images/bg-2.png" -->

## Preface

Browser requirements
- Any _modern_ browser will work (IE 11+)
- Mobile: _latest_ Samsung & Apple devices
- Dedicated graphics card recommended

---

<!-- .slide: data-background="images/bg-2.png" -->

## Agenda

1. Getting Started
2. Adding Data
3. Visualizing Data
4. Interacting with Data
5. Web Scenes

---

<!-- .slide: data-background="images/bg-4.png" -->

## Getting Started

---

### ToDo

- Widgets, e.g. search

---

<!-- .slide: data-background="images/bg-3.png" -->

### The simplest possible app

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Create a 3D map</title>  
  
  <link rel="stylesheet" href="//js.arcgis.com/4.10/esri/css/main.css">
  <script src="//js.arcgis.com/4.10/"></script>  
  
</head>
<body>
  <script>
      require([
        "esri/Map",
        "esri/views/SceneView",
        "dojo/domReady!"
      ], function(Map, SceneView) {
        
        var map = new Map({
          basemap: "satellite"
        });
        
        var view = new SceneView({
          container: "viewDiv",
          map: map
        });        
      });
  </script>
  <div id="viewDiv"></div> 
</body>
</html>
```

<span style="font-size: 50%">https://developers.arcgis.com/javascript/latest/sample-code/sandbox/index.html?sample=intro-sceneview</span>

---

### The simplest possible app

- Out of the box you get:
  - 3D rendering of the world
  - User interaction with the 3D view (navigation)
  - A set of basemaps to work with
  - 3D terrain

---

<!-- .slide: data-background="images/bg-3.png" -->

### Architecture

<br/>
<img src="images/architecture-map-sceneview-layers.png" width="60%" style="border: none; background: none; box-shadow: none"/>

---

<!-- .slide: data-background="images/bg-3.png" -->

### Changing a map from 2D to 3D

- [`Map`](https://developers.arcgis.com/javascript/latest/api-reference/esri-Map.html) is universal
- [`MapView`](https://developers.arcgis.com/javascript/latest/api-reference/esri-MapView.html) creates a 2D map
- [`SceneView`](https://developers.arcgis.com/javascript/latest/api-reference/esri-SceneView.html) creates a 3D map

<span style="font-size: 50%">https://developers.arcgis.com/javascript/latest/sample-code/sandbox/index.html?sample=layers-vectortilelayer</span>
---

<!-- .slide: data-background="images/bg-4.png" -->

## Resources

<ul>
  <li>Developer portal (SDK)</li>
  <li>Sandbox</li>
  <li>GitHub</li>
  <li>Pricing?</li>
</ul>

---

<!-- .slide: data-background="images/bg-4.png" -->

## Adding Data

---

### Projections

[SceneView.viewingMode](https://developers.arcgis.com/javascript/latest/api-reference/esri-views-SceneView.html#viewingMode)

<table>
  <tr>
    <td style="vertical-align: middle">
      Global scene:<br/>
      <ul>
        <li>WebMercator</li>
        <li>WGS84</li>
      </ul>  
    </td>
    <td>
      <img src="images/global-scene.jpg" width="405px"/>
    </td>
  </tr>
  <tr>
    <td style="vertical-align: middle">
      Local scene:<br/>
      <ul>
        <li>Any projected CS</li>
        <li>One PCS only!</li>
      </ul>  
    </td>
    <td>
      <img src="images/local-scene.jpg" width="405px"/>
    </td>
  </tr>
</table>
---

<!-- .slide: data-background="images/bg-3.png" -->

### ToDo

- Add a `TileLayer`
  - https://services.arcgisonline.co.nz/arcgis/rest/services/Imagery/newzealand/MapServer
  - Discuss adding as op layer vs basemap?  
- Add buildings (3D object scene layer, not BSL)
  - Data sources: living atlas, portal item, URL
- Add point features
  - FeatureLayer and/or GeoJSON/CSV?
- Overview of layer/data types

---

<!-- .slide: data-background="images/bg-4.png" -->
## Visualizing Data

---

### ToDo

- ~~Theoretical background on Renderers/Symbols~~
- Change building style
  - Textures on/off
  - Edges
- Change point style
  - From primitive to web style icon
  - Callouts, maybe perspective
  - Add tree layer + 3D models from web styles?
- elevationInfo? 

---

### Renderers and Symbols

- Use the same renderers in 2D and 3D
  - [`SimpleRenderer`](https://developers.arcgis.com/javascript/latest/api-reference/esri-renderers-SimpleRenderer.html), [`ClassBreaksRenderer`](https://developers.arcgis.com/javascript/latest/api-reference/esri-renderers-ClassBreaksRenderer.html), [`UniqueValueRenderer`](https://developers.arcgis.com/javascript/latest/api-reference/esri-renderers-UniqueValueRenderer.html)
- 2D symbols are supported, _lossy conversion_
- For 3D visualizations, use 3D symbols
  -  [`PointSymbol3D`](https://developers.arcgis.com/javascript/latest/api-reference/esri-symbols-PointSymbol3D.html), [`LineSymbol3D`](https://developers.arcgis.com/javascript/latest/api-reference/esri-symbols-LineSymbol3D.html), [`PolygonSymbol3D`](https://developers.arcgis.com/javascript/latest/api-reference/esri-symbols-PolygonSymbol3D.html), [`MeshSymbol3D`](https://developers.arcgis.com/javascript/latest/api-reference/esri-symbols-MeshSymbol3D.html)

---

### 3D Symbols

<!-- (flat) IconSymbol3DLayer - LineSymbol3DLayer - FillSymbol3DLayer -->

<table class="symbology">
  <tr>
    <th>PointSymbol3D</th>
    <th>LineSymbol3D</th>
    <th>PolygonSymbol3D</th>
  </tr>
  <tr>
    <td>
      <div class="image-title">IconSymbol3DLayer</div>
      <img src='./images/isl.png' width='310'/>
    </td>
    <td>
      <div class="image-title">LineSymbol3DLayer</div>
      <img src='./images/lsl.png' width='310'/>
    </td>
    <td>
      <div class="image-title dark">FillSymbol3DLayer</div>
      <img src='./images/fsl.png' width='310'/>
    </td>
  </tr>
  <tr>
    <!-- (volumetric) ObjectSymbol3DLayer - PathSymbol3DLayer - ExtrudeSymbol3DLayer -->
    <td>
      <div class="image-title">ObjectSymbol3DLayer</div>
      <img src='./images/osl.png' width='310'/>
    </td>
    <td>
      <div class="image-title">PathSymbol3DLayer</div>
      <img src='./images/psl.png' width='310'/>
    </td>
    <td>
      <div class="image-title">ExtrudeSymbol3DLayer</div>
      <img src='./images/esl.png' width='310'/>
    </td>
  </tr>
</table>

---

<!-- .slide: data-background="images/bg-4.png" -->

## Interacting with Data

---

### ToDo

- Introduce BSL
- Interacting with BSL: hitTest -> hide layer
- goTo 

---

<!-- .slide: data-background="images/bg-4.png" -->

## WebScene
### _Loading and saving your scene_

---

### WebScene
#### _Remember:_
<br/>
<img src="images/architecture-map-sceneview-layers.png" width="60%" style="border: none; background: none; box-shadow: none"/>

---

### WebScene

<img src="images/architecture-map-webscene-sceneview-layers.png" width="60%" style="border: none; background: none; box-shadow: none"/>

---

### WebScene
<br/>
<img src="images/architecture-map-webscene.png" width="60%" style="border: none; background: none; box-shadow: none"/>
<br/>
<br/>

<div class="twos" style="font-size: 80%">
  <div style="margin-left: 4em">
    <ul>
      <li>Works with `MapView` and `SceneView`</li>
      <li>Cannot be saved</li>
    </ul>   
  </div>
  
  <div>
    <ul>
      <li>Only works with `SceneView`</li>
      <li>Can be saved to Online/Enterprise</li>
    </ul>   
  </div>
  
</div>

---

### WebScene
#### _Loading a scene_

```javascript
require([
  "esri/WebScene",
  "esri/views/SceneView",
  "dojo/domReady!"
], function(WebScene, SceneView) {
  
  var scene = new WebScene({
    portalItem: {
      id: "19dcff93eeb64f208d09d328656dd492"
    }
  });
  
  var view = new SceneView({
    container: "viewDiv",
    map: scene
  });
});
```

<span style="font-size: 50%">https://developers.arcgis.com/javascript/latest/sample-code/sandbox/index.html?sample=webscene-basic</span>

---

### WebScene
- Save to ArcGIS Online or Enterprise ([SDK sample](https://developers.arcgis.com/javascript/latest/sample-code/webscene-save/index.html))
- Persists _data_, not _view_ or _app behavior_
- ...with some exceptions, for example:
  - Popup behavior
  - Initial view
- JSON specification similar to WebMap
  - https://developers.arcgis.com/web-scene-specification/

---

<!-- .slide: data-background="images/bg-4.png" -->

## Where to?

---

<!-- .slide: data-background="images/bg-2.png" -->

### Related sessions

- Interactive 3D Maps with the JavaScript API: _Beyond the Basics_ <br/>
  _Wed 5.30pm, Primrose B_
- Practical Guide for Building a 3D Web App From 2D Data<br/>
  _Thu 10.30am, Primrose A_
- 3D Visualization with the ArcGIS API for JavaScript<br/>
  _Thu 4pm, Primrose C-D_

---

<!-- .slide: data-background="images/bg-survey.jpg" -->

---

<!-- .slide: data-background="images/bg-esri.png" -->
