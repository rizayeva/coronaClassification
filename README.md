# Historical Corona satellite imagery classification within GEE


  
  **Generate a point grid for further data collection**
  
  Import the point grid in GEE as FeatureCollection (Assets -> New -> Shape files). Be sure to add all auxiliary files and not only .shp

Import the images to GEE (with correct projection and 1 band). The rasters can be too large for GEE, but you can also apply a JPEG or LZW compression. For this, use OSGeo and follow the steps in **shellCode1**

Use the code in **Code1** to export the objects corresponding to the point grid locations within the image of interest. To view a sample of the results for Step1 please use the following link:

https://rizayeva.users.earthengine.app/view/step1

After exporting the objects, overlay them with the point grid on your local workstation and label the land cover classes by creating a new "Classes" column.

You may also want to create a column to take notes about the quality of the objects. Pure objects can be used for training and validation, while mixed (over-segmented) or shifted objects can only be used for validation.


Use the code in **Code2** to calculate second-order texture metrics from Corona imagery. 

Follow the instructions within the code
If you decide to divide your image in several geometries, you may start with a larger size geometry first and then if processing results in an error, you may decrease the size. With time, the sizes of the geometries will be intuitive. For reference, check the sizes of my geometries within the same code.

If you divided your image into several geometries, then also use code in **Code2.1** to merge the separate exported texture layers into one for each of the chosen second-order texture metrics. 


Use the code in **Code3** to run ten fold object-based classification of Corona data with incorporation of DEM. 

Use previously exported objects for visual identification only. Do not import objects as training/testing data, since this will fail and even if it does not, it would overestimate the classes with larger objects)
**Separate 80/20% Training/testing data:**


Select randomly 80% of the points overlapping with pure objects and export them as TrainingMMDDYYYY_1, TrainingMMDDYYYY_2, …, TrainingMMDDYYYY_10 (shapefiles)

If you decide to add more points for poorly represented classes, only add them to Training data.

Export the remaining 20% of the points to later be used for testing as TestMMDDYYYY_1, TestMMDDYYYY_2, …, TestMMDDYYYY_10 (shapefiles)

Export 20% of points overlappping with mis-segmented objects (over-segmented specifically) and 20% from shifted objects.

Merge the three layers and export them as TestingMMDDYYYY_1, TestingMMDDYYYY_2, …, TestingMMDDYYYY_10 (shapefiles)

Always check the number of points in the resulting shapefiles to prevent any errors

Import the point data in GEE in separate folders for *Training* and *Testing*. 

GEE -> Assets -> New -> Shapefiles: Drag and drop each set one-by-one (5 files for TrainingMMDDYYYY_1, then 5 files for TestingMMDDYYYY_1, etc.); add the Folder name in front of the Asset name (would look like: Training/TrainingMMDDYYYY_1); Click “Upload”

Import labeled points in GEE

Follow the instructions provided in the beginning of the code 

Due to memory limits depending on the size of your study area, the resulting maps may not be possible to visualize right away. In that case please export the maps and the accuracy results to Assets or Drive


To visualize the results of classification and the accuracy assessments for each  method used in our paper, please use the following the link:
https://rizayeva.users.earthengine.app/view/coronaclassificationvisualization


Should you have any questions, do not hesitate to reach out via: rizayeva@wisc.edu

For reference:
Rizayeva, A., Nita, M.D., Radeloff, V.C., 2022 **(?)**, Large-area, 1964 land cover classifications of Corona spy satellite imagery for the Caucasus Mountains, *Remote Sensing of Environment*, 248, 111967.
