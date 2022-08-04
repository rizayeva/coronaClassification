# Historical Corona satellite imagery classification within GEE


  
  Generate a point grid for further data collection
  
  Import the point grid in GEE as FeatureCollection (Assets -> New -> Shape files). Be sure to add all auxiliary files and not only .shp

Import the images to GEE (with correct projection and 1 band):

The files can be too large for GEE, but you can also apply a JPEG or LZW compression. For this, use OSGeo and follow the steps in shellStep1

Set the correct date when uploading in GEE


Use the code in Step1 to export the objects corresponding to the point grid locations within the image of interest. To view a sample of the results for Step1 please use the following link:

https://rizayeva.users.earthengine.app/view/step1


Use the code in Step2 to calculate second-order texture metrics from Corona imagery. 


Use the code in Step3 to merge the separate exported texture layers into one for each of the chosen second-order texture metrics. 


Use the code in Step4 to run ten fold object-based classification of Corona data with incorporation of DEM. 


To visualize the results of classification and the accuracy assessments for each  method, please use the following the link:
https://rizayeva.users.earthengine.app/view/coronaclassificationvisualization


