---
title: "Maps"
permalink: "/documentation_spike"
---

## Introduction

This tutorial is a detailed introduction to the [Maps API for JavaScript 3.1](https://developer.here.com/documentation/maps/topics/quick-start.html).

The Maps API for JavaScript was refreshed in 2019 to include some key new features:
- vector rendering
- customization of the map's look and feel
- runtime change of the map style
- ability to hide/show base map data layers at the runtime
- map tilting and rotation
- extruded buildings
- fractional zoom levels
- interactive traffic flow information
- rich interactions with the map - retrieve feature's meta information
- introduction of APIKey as new authentication method

In this tutorial, you will create a feature-rich isoline routing visualization application.

   ![Sample Image](https://images.pexels.com/photos/112460/pexels-photo-112460.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500)
   
The template code is provided so you can focus on implementing the Maps API code instead of focusing on trivial details like CSS.

When you download and unzip the template, you'll see the following file structure:

```
|--template
   |--index.html
   |--css
      |--index.css
      |--search.css
      |--sidebar.css
   |--js
      |--app.js
      |--config.js
      |--helpers.js
   |--resources
      |-- ...
      |-- ...
```
    
### Some notes on helper functions
   
  <iframe width="560" height="315" src="https://www.youtube.com/embed/54J_ZCbeJdc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 
 In the code above, we've:
 
 - initialized the platform and basic interactive map.
 - added behavior controls and events. This way we can pan around the map. Try holding down either option (Mac) or alt (Windows) to have fun panning around the map in 3D!
 - initialize the router and geocoding service. We'll be using these later on in the tutorial.
 - added an event listener to the window to make sure the map resizes when the browser changes sizes.
 
 If you save the file and refresh, you'll see a basic map up and running!
 
## Initialize the platform and map {#initialize-map}

   <iframe width="100%" height="300" src="//jsfiddle.net/itsmelibin/0nah92p7/embedded/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

Let's get started by adding the Maps API for JavaScript imports.

Inside of `index.html` add the following script imports to your document's `<head>`:


__index.html__
```html
<!-- JS API -->
<link rel="stylesheet" type="text/css" href="https://js.api.here.com/v3/3.1/mapsjs-ui.css" />
<script src="https://js.api.here.com/v3/3.1/mapsjs-core.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-service.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-ui.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-mapevents.js"></script>
```
  
We'll need to import the `router` from our main `app.js` file so it can be used here. 

We create the function `requestIsolineShape` that will make the request to the HERE Routing API for us. The JavaScript API conveniently wraps this request for us with the `router.calculateIsoline()` option.

The function we've made, `requestIsolineShape()`, will return a promise that will get resolved once the response from the HERE server is made. 

 <html>
    <head>
      <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
      <script type="text/javascript">
        google.charts.load("current", {packages:["corechart"]});
        google.charts.setOnLoadCallback(drawChart);
        function drawChart() {
          var data = google.visualization.arrayToDataTable([
            ['Task', 'Hours per Day'],
            ['Work',     11],
            ['Eat',      2],
            ['Commute',  2],
            ['Watch TV', 2],
            ['Sleep',    7]
          ]);
  
          var options = {
            title: 'My Daily Activities',
            is3D: true,
          };
  
          var chart = new google.visualization.PieChart(document.getElementById('piechart_3d'));
          chart.draw(data, options);
        }
      </script>
    </head>
    <body>
      <div id="piechart_3d" style="width: 900px; height: 500px;"></div>
    </body>
  </html>

We'll pass it a few different parameters, all of which will be configured by the application user from the sidebar UI.
- __mode__: choice between `pedestrian`, `car`, or `truck`. This parameter will also contain the flag to enable traffic or not.
- __start__: the coordinates of the isoline center point.
- __range__: the range isoline. Example: 4000.
- __rangetype__: distance (meters) or time (seconds).
- __departure__: if traffic is enabled, the date and time of departure.

For more example on isoline routing, we have a few blog posts available on the topic:

- [Finding my dream home with isoline routing](https://developer.here.com/blog/finding-my-dream-home-with-isoline-routing)
- [Interactive isoline grid with HERE + React + Leaflet](https://developer.here.com/blog/interactive-isoline-grid-with-here-react-leaflet)

...or check out the [official documentation](https://developer.here.com/documentation/routing/topics/request-isoline.html).
   
 <iframe width="700" height="500" src="https://codepen.io/itsmelibin/pen/ZEEaWwG" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
   