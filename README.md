# Historical Corona satellite imagery classification within GEE


  
  **Generate a point grid for further data collection**
  
  Import the point grid in GEE as FeatureCollection (Assets -> New -> Shape files). Be sure to add all auxiliary files and not only .shp

Import the images to GEE (with correct projection and 1 band). The rasters can be too large for GEE, but you can also apply a JPEG or LZW compression. For this, use OSGeo and follow the steps in **shellStep1**

Set the correct date when uploading in GEE


Use the code in **Step1** to export the objects corresponding to the point grid locations within the image of interest. To view a sample of the results for Step1 please use the following link:

https://rizayeva.users.earthengine.app/view/step1

After exporting the objects, overlay them with the point grid on your local workstation and label the land cover classes by creating a new "Classes" column.

You may also want to create a column to take notes about the quality of the objects. Pure objects can be used for training and validation, while mixed (over-segmented) or shifted objects can only be used for validation.


Use the code in **Step2** to calculate second-order texture metrics from Corona imagery. 

Follow the instructions within the code
If you decide to divide your image in several geometries, you may start with a larger size geometry first and then if processing results in an error, you may decrease the size. With time, the sizes of the geometries will be intuitive. For reference, check the sizes of my geometries within the same code.

If you divided your image into several geometries, then also use code in **Step2.1** to merge the separate exported texture layers into one for each of the chosen second-order texture metrics. 


Use the code in **Step4** to run ten fold object-based classification of Corona data with incorporation of DEM. 
Import labeled points in GEE in separate folders for *Training* and *Testing*. Use previously exported objects for visual identification only. Do not import objects as training/testing data, since this will fail and even if it does not, it would overestimate the classes with larger objects)
Adjust the following variables: **palette**

Separate 80/20% Training/testing data
Select randomly 80% of the points (Vector -> Research Tools -> Random selection: Input - grid5km_label_07142020_EPSG32638_1024-2104_ClassesJ_wObj_TRonly.shp; Method – Percentage of selected features; Number/perentage – 80 -> Run), export selected features and call them TrainingMMDDYYYY_1, TrainingMMDDYYYY_2, …, TrainingMMDDYYYY_10 (shapefiles; in my case: \\haven\Data\afarizayeva\PhD_Madison2\Chapter II\Analyses\1024-2104\BasedOnTR\Training01172022_1.shp)
Invert the selection each time (Attribute table -> invert selection) and export the selected 20% of the points to later be used for testing; export and call them TestingMMDDYYYY_1, TestingMMDDYYYY _2, …, TestingMMDDYYYY _10 (shapefiles)
Check the resulting files just in case to make sure that the number of points in each is corresponding to the 80/20 rule and that there was no error
Now we can remove the 10 pairs of Training and Testing shapefiles added to QGIS automatically
Import the training data in GEE to the folder Training_Testing_1024-2104
GEE -> Assets -> New -> Shapefiles: Drag and drop each set one-by-one (5 files for TrainingMMDDYYYY_1, then 5 files for TestingMMDDYYYY_1, etc.); add the Folder name in front of the Asset name (in my case: Training_Testing_1024-2104/TrainingMMDDYYYY_1); Click “Upload”

To visualize the results of classification and the accuracy assessments for each  method, please use the following the link:
https://rizayeva.users.earthengine.app/view/coronaclassificationvisualization


Should you have any questions, do not hesitate to reach out via: rizayeva@wisc.edu

For reference:
Rizayeva, A., Nita, M.D., Radeloff, V.C., 2022 **(?)**, Large-area, 1964 land cover classifications of Corona spy satellite imagery for the Caucasus Mountains, *Remote Sensing of Environment*, 248, 111967.
