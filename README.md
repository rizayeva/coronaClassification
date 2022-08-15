

<h1 style="color:green;"> Historical Corona satellite imagery classification within GEE </h1>
    
```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```

  **Generate a point grid.**
  
  Import the point grid in GEE as a FeatureCollection (Assets -> New -> Shape files). Be sure to add all auxiliary files and not only the .shp file.

Import the images to GEE (with the correct projection and 1 band). If the rasters are too large for GEE, apply a JPEG or LZW compression. For this, use OSGeo and follow the steps in **shellCode**.

Use the code in **traObjExp** to export the objects corresponding to the point grid locations within the image. <a target="_blank" href="https://rizayeva.users.earthengine.app/view/step1">Click here</a> to view a sample of the results for **traObjExp**.

After exporting the objects, overlay them with the point grid on your local workstation and label the land cover classes by creating a new "Classes" column in the point shapefile.

You may also want to create a column to take notes about the quality of the objects. Pure objects can be used for training and validation, while mixed (over-segmented) or shifted objects can only be used for validation.


Use the code in **texCal** to calculate second-order texture metrics from Corona imagery. They will later be used as input layers for object-oriented classification.

Follow the instructions within the code.

If you decide to divide your image into several geometries, you may start with a larger size geometry first and if processing results in an error, you may decrease the geometry size. With time, the sizes of the geometries will be intuitive. For reference, check the sizes of my geometries within the same code.

If you divided your image into several geometries, use the code in **texMer** to merge the separate exported texture layers into one texture layer for each of the chosen second-order texture metrics. 


Use the code in **OBIA_10111040_10fold** to run a ten-fold object-oriented classification of Corona data with a DEM. 

Use previously exported objects for visual identification only. Do not import objects as training/testing data, since this will either fail, or overestimate the classes with larger objects).

**Separate 80/20% Training/testing data (will be done 10 times):**


Select randomly 80% of the points overlapping with pure objects and export them as TrainingMMDDYYYY_1, TrainingMMDDYYYY_2, …, TrainingMMDDYYYY_10 (shapefiles).

If you decide to add more points for poorly represented classes, only add them to Training data.

Export the remaining 20% of the points to later be used for testing as TestMMDDYYYY_1, TestMMDDYYYY_2, …, TestMMDDYYYY_10 (shapefiles).

Export 20% of points overlapping with mis-segmented objects (over-segmented specifically) and 20% from shifted objects.

Merge the three layers (test, mis-segmented and shifted) and export them as TestingMMDDYYYY_1, TestingMMDDYYYY_2, …, TestingMMDDYYYY_10 (shapefiles).

Always check the number of points in the resulting shapefiles to prevent any errors.

**Import labeled points in GEE.**

Import the point data in GEE in separate folders for *Training* and *Testing*. 

GEE -> Assets -> New -> Shapefiles: Drag and drop each set one-by-one (10 files for TrainingMMDDYYYY_1, then 10 files for TestingMMDDYYYY_1, etc.); add the Folder name in front of the Asset name (would look like: Training/TrainingMMDDYYYY_1); Click “Upload”.

Follow the instructions provided in the beginning of the code. 

Due to memory limits depending on the size of your study area, the resulting maps may not be possible to visualize right away. In that case please export the maps and the accuracy results to Assets or Drive.


<a target="_blank" href="https://rizayeva.users.earthengine.app/view/coronaclassificationvisualization">Click here to visualize</a> the results of the classification and the accuracy assessments for each  method used in our paper.


Should you have any questions, do not hesitate to reach out: rizayeva@wisc.edu

For reference:
Rizayeva, A., Nita, M.D., Radeloff, V.C., 2022 **(?)**, Large-area, 1964 land cover classifications of Corona spy satellite imagery for the Caucasus Mountains, *Remote Sensing of Environment*.
