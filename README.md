# I've joined the #100DaysOfCode Challenge

## Day 0: 5th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-0-code-to-download-satellite-imagery.ipynb

**Today's Progress:** Downloaded Sentinel imagery. GeoJSON produced in QGIS, downloaded imagery viewed in QGIS. 
I have used sentinelsat, pandas and os libraries. 

**Thoughts:**
- I have used the sentinelsat api to query and download data from the Copernicus Access Hub (https://scihub.copernicus.eu/dhus/#/home) before at work and found it worked well. The source code on Sentinelsat GitHub account shows recent commits. 
- It is important to save my login details for the Copernicus Access Hub as environmental variables so as not to give away password information.
- I want to use Pathlib rather than os.path.join because it slicker, much simplier and comes with much more functionality, see this post: https://pbpython.com/pathlib-intro.html
- Time has been spend fixing QGIS in this session, I had dependency issues and aptitude saved the day. 

**Tomorrows plans:** Visualisation of the imagery data. Look at gdal, rasterio and skimage. 

![day 1](https://github.com/datalass1/100-days-of-code/blob/master/images/day1-QGIS-downloaded-imagery.png?raw=true)


### Day 1: 6th April

Inspiration: https://github.com/scikit-image/skimage-tutorials and https://www.youtube.com/watch?v=pZATswy_IsQ

# Some of my most used code and links
- while read requirement; do conda install --yes $requirement; done < requirements.txt https://gist.github.com/luiscape/19d2d73a8c7b59411a2fb73a697f5ed4

