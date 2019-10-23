# simplify-geojson-readme

**To simplify geojson:**

1. Wrap json features into a “FeatureCollection” object

2. Validate data as a geojson
    - [Mapshaper](https://mapshaper.org/)
    - [Geojson-validation library](https://www.npmjs.com/package/geojson-validation)
        i. It has a CLI tool to validate geojson. When the output is valid it will return with `valid`
        
 3. Trim geojson with [simplify-geojson](https://www.npmjs.com/package/simplify-geojson)
   - It applies the  Ramer–Douglas–Peucker line simplification algorithm to GeoJSON features or feature collections in JS or        on the CLI.
      After installation: 
      
      **CLI**
      
       `cd` into the directory with the geojson or json data
      
       `cat data.geojson | simplify-geojson -t 0.01`
       
       `-t` indicates the tolerance 
       
      **JS** 
      
      
     ``` 
       const simplify = require('simplify-geojson')
       const simplified = simplify(geojson, tolerance) 
     ```
      
      
     `geojson` can be any valid "Feature" or "FeatureCollection"
     
     **To save the output**
     
     
     ```
     const geojson = require('data.json')
     const simplify = require('simplify-geojson')
     const simplified = simplify(geojson, 0.01)
     const fs = require('fs');

     let data = JSON.stringify(simplified);
     fs.writeFileSync('somedata.json', data);
    ```
     
     
   4. Use again Mapshaper or the Geojson-validation library to confirm that the generated geojson is valid!
   
   
   **To convert to tiles**
   
   1. Install mapbox tippecanoe
   
   2. `cd` into the directory that includes the json or geojson files
   
   3. run the following command
      `tippecanoe -zg -o out.mbtiles --drop-densest-as-needed in.geojson`
      
      `out.mbtiles` is the output 
      
      `in.geoson` is the file that you want to convert to tiles
      
      `--drop-densest-as-needed` option will make Tippecanoe try dropping what should be the least visible features at each          zoom level (suggested when you aren't sure of what options to use)
      
   4. Files are ready to be uploaded on Mapbox Studio 
      
      
   
   For more geojson tools and resources: https://github.com/tmcw/awesome-geojson
    



