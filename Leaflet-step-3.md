In Leaflet step 3 we will add a GeoJSON file containting geospatial data to our map.

### GeoJSON
GeoJSON is the standard data type to create web maps with. You can add this data as another map layer.
The geodata that we want to add will be a GeoJSON file. JSON stands for JavaScript Object Notation. GeoJSON is a format for encoding a variety of geographic data structures.

This is how it looks like:

``` JSON
{
  "type": "Feature",
  "geometry": {
   "type": "Point",
   "coordinates": [125.6, 10.1]
  },
  "properties": {
   "name": "Dinagat Islands"
  }
}
```

GeoJSON supports the following geometry types: `Point, LineString, Polygon, MultiPoint, MultiLineString, and MultiPolygon`. Geometric objects with additional properties are Feature objects. Sets of features are contained by FeatureCollection objects.

It uses the World Geodetic System 1984, and units of decimal degrees.

More links and info can be found in [[Tips & Tricks]]


### Let's add the Squatch Watch Data to our map!

:arrow_forward: Download the dataset from https://github.com/NieneB/Webmapping_for_beginners/tree/gh-pages/data

:arrow_forward: Place the All_BFRO_Reports_points.geojson file in `yourDirectory`.

:arrow_forward: Copy the following script and have a look at your map.

``` js
// Create a marker first
var geojsonMarkerOptions = {
    radius: 8,
    fillColor: "#ff7800",
    color: "#000",
    weight: 1,
    opacity: 1,
    fillOpacity: 0.8
};

//create the geojson layer
var geojson = L.geoJson(geojsonFeature,{
  pointToLayer: function (feature, latlng) {
    return L.circleMarker(latlng, geojsonMarkerOptions);
  }
}).addTo(map);

//add your geojson data to the layer
var xhr = new XMLHttpRequest();
xhr.open('GET', encodeURI("All_BFRO_Reports_points.geojson"));
xhr.onload = function() {
if (xhr.status === 200) {
    geojson.addData(JSON.parse(xhr.responseText));
  } else {
    alert('Request failed.  Returned status of ' + xhr.status);
  }
};
xhr.send();
```

If we want to add our own spatial data to our map, we need to run a local server.

### Running a local server

When developing a website, a web designer needs to be able to see his webpages the same way the end user would. Sometimes simply clicking on and viewing your HTML files in the web browser is enough, but if you want to test dynamic content, you will need to set up a local web server. Doing this is quite simple and can easily be accomplished on Windows, Mac, and Linux. There are many types of web servers available, but we will be using the Python's SimpleHTTPServer as it is very easy to set up.

http://www.pythonforbeginners.com/modules-in-python/how-to-use-simplehttpserver/
https://www.maketecheasier.com/setup-local-web-server-all-platforms/



Easy ways of doing this include running Python's SimpleHTTPServer in your map directory, installing MAMP (for Mac), or installing WampServer (for Windows). 

:arrow_forward: To start a HTTP server on port 8000 (which is the default port), simple type:

```
python -m SimpleHTTPServer [port]
```

Oef! But where?! 
Let's start from the beginning:

 :arrow_forward: Open a Terminal. `Menu > Terminal`

If you have never done this before it might look a bit scary.. But don't worry. There is nothing we will do that will ruin your computer! We will start with the 3 most important navigation tools for the Terminal. Just image the Terminal is like your File Browser, but then without the interface.

:information_source: `pwd` means Print Working Directory. It will answer with the location that we are currently in. Try it:

:arrow_forward: Type `pwd` in the terminal and press enter! 

Probably you are in your home directory. 

:information_source: `ls` will LiSt all the files in your current directory. 

:arrow_forward: Type `ls` in the terminal and press enter! Do you see all the files and folders of your current working directory?

:information_source: `cd [directory]` stands for Change Directory and will navigate you to the next directory you told it to. 

:arrow_forward: If you have a folder named `Documents`, (check with `ls`) then type `cd Documents/` in the terminal and press enter! 

If we would type 'pwd' again, you can see that you changed from your home directory to you Documents directory. 
If you want to go back up the working tree we can use `cd ..` to move 1 folder up.

:arrow_forward: Type `cd ..` and press enter. Check with `pwd` where you are now. 

Using all this information we can browse to `YourDirectory` where the `index.html` and the GeoJSON file is.

:arrow_forward: Using `cd` go to `Yourdirectory`. 

This is where we will run our local server! 

:arrow_forward: To start a HTTP server on port 8000 (which is the default port), simple type:

```
python -m SimpleHTTPServer [port]
```








The following map is was also made from this dataset. For inspiration:

![bigfoot](http://thumbnails.visually.netdna-cdn.com/SquatchWatch92YearsofBigfootSightingsintheUSandCanada_523b7482cc497.png)


:arrow_right: Continue to [[Introduction D3]] or do the [[Leaflet Advanced assignments]]
