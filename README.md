# geeMosaics
A jupyter notebook to create composite mosaics from Sentinel-2 MSI Surface Reflectance imagery. 

This script is in progress. I am working on adding an alpha band to the mosaics for posting to WMS/WMTS.

Methodology
---------------------
1. Search for Sentinel-2 SR imagery for a specific area and pre-defined time range
2. Mask clouds
3. Multiply by 0.0001 and calculate median of the entire collection
4. Apply a stretch and visualization parameters 
5. Scale, valid data data range (1-255, no data is 0)
6. Convert to 8-bit
7. Export true color or false colour RGB in geotiff format as tiles
8. Mosaic tiles (once downloaded)

Installation
---------------------
Sign up for a Google Earth Engine account if you don't already have one (https://signup.earthengine.google.com/). 

Install Anaconda (https://docs.anaconda.com/free/anaconda/install/windows/).

In Anaconda Prompt, create a new environment called gee.
```
conda create -n gee python=3.10
```
Activate it,
```
conda activate gee
```
And then install mamba.
```
conda install mamba -c conda-forge
```
Using mamba install geemap and supporting packages from the conda-forge channel.
```
mamba install geemap geopandas localtileserver python -c conda-forge
```
To learn more about the amazing geemap package please visit the following github page (https://github.com/gee-community/geemap).

Install gcloud CLI
---------------------
Follow the instructions from https://cloud.google.com/sdk/docs/install to install Google Cloud CLI. Use the same email address as for Google Earth Engine.

You may need to independently authorize gcloud in Anaconda:
```
gcloud auth login
```
To check which account is being used, in Anaconda type in
```
gcloud auth list
```

Install gdal
---------------------
Installing gdal can be challenging. The following works for me but your millage may vary. 

Go to Chrisoph Gohlke's GitHub page (https://github.com/cgohlke/win_arm64-wheels), scroll down to Assets and download the .whl.zip file. Copy the appropriate gdal wheels (ex.GDAL-3.9.0-cp312-cp312-win_arm64.whl) to your machine. 

Then go back to Anaconda Prompt, make sure that you are in the gee environment (conda activate gee) and install gdal into the gee environment.
```
pip install <path to wheels> 
```
In my case it was:
```
pip install C:\Users\Downloads\2024.6.15-experimental-cp312-win_arm64.whl\2024.6.15-experimental-cp312-win_arm64.whl\GDAL-3.9.0-cp312-cp312-win_arm64.whl.
```
Open python:
```
python
```
Import gdal:
```
from osgeo import gdal
```
Import GEE:
```
import ee 
```
And authenticate GEE.
```
ee.Authenticate()
```
Follow instructions to authenticate gee, you will be lead to a webpage. Once the account has been authenticated you should be ready to go. The message should read "You are now authenticated with gCloud CLI". To get out of the python commands in Anaconda press Ctrl + Z or exit().

A note on gdal
---------------------
If the above installation doesn't work for you, there are a number of solutions presented in various forums and articles. 

Warning! Some will suggest to disable your SSL certificate verification to install gdal. You can do this, but you may break other packages that require SSL verification and/or upset your IT department. 

Running the notebook 
---------------------
In Anaconda, run jyputer notebook. A new window will open, locate and double click on the notebook. 

As always, many thanks to the open source community!
---------------------
Wu, Q., (2020). geemap: A Python package for interactive mapping with Google Earth Engine. The Journal of Open Source Software, 5(51), 2305. https://doi.org/10.21105/joss.02305
