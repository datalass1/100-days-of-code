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
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-1-visualising-imagery.ipynb

**Today's Progress:** Pre-process Sentinel-2 1C imagery to stack 10m bands 2,3,4,8 and visualise each individual band 

**Thoughts:** The Geospatial Data Abstraction Library (GDAL) is a great library for reading and writing raster and vector data. It supports Sentinel data and I was able apply gdal_translate to change JP2000 to tif for the 10m bands and then gdal_merge with seperate to stack the imagery. Finally using rasterio to read in the stacked tif and visualise each individual band. 

**Tomorrows plans:**
More visualisation and exploratory data analysis of Sentinel imagery. I would like to try displaying the RGB and False colour images, as well as some image manipulation. I wonder if these tutorials coule be applied: Inspiration: https://github.com/scikit-image/skimage-tutorials and https://www.youtube.com/watch?v=pZATswy_IsQ

![day_2](https://github.com/datalass1/100-days-of-code/blob/master/images/day2-image-bands.png?raw=true)

### Day 2: 7th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-2-skimage-numpys-and-visualisation.ipynb

**Today's Progress:** Using scikit image to work with imagery data as numpy arrays, pre-processing for matplotlib visualisation by normalising and equalising the Sentinel-2 imagery.

**Thoughts:** The Sentinel-2 imagery of Madagascar is in uint16 and imageio.core.util.Image dtype when opened with scikit-image. This makes visualisation a challenge, why: because the np.stack for creating the true and false coloured images wanted an unint8 and numpy arrary. So I changed the data by normalising it and equalising it with a contrast stretch. I think this was the right thing to do, and it worked!

- unsigned 16-bit integer image range is [0, 65535] When using ```image.astype(np.uint8)``` noise would be introduced to the image. By using ```img_as_float``` a floating point image with range [0, 1] is created to preserve the information. 
- Equalisation required to increase image contrast: http://scikit-image.org/docs/dev/auto_examples/color_exposure/plot_equalize.html I used contrast stretching. 
- Memory kept running out on the Acer laptop. 
- Learning about matplotlib axes, especially when it comes to subplots. 

**Tomorrows plans:** Keep going through the https://github.com/scikit-image/skimage-tutorials and https://www.youtube.com/watch?v=pZATswy_IsQ - more work on numpy arrays with scikit-image. 

![cat](https://github.com/datalass1/100-days-of-code/blob/master/images/day3-HIcat.png?raw=true)
![true_false_imagery](https://github.com/datalass1/100-days-of-code/blob/master/images/day3_true_false_color_images.png?raw=true)

### Day 3: 8th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day3-image-filtering-removing-noise-from-arrays.ipynb

**Today's Progress:** Using numpy and scipy on arrays to remove noise. Two techniques explored: averaging with nearest pixel
and convolution. 

**Thoughts:** Convolution is HARD! I looked at Khan Acadmeys video 'Introduction to Convolution' and it is rather mathematical. I found Ian Goodfellows book on Deep Learning: https://www.deeplearningbook.org/contents/convnets.html and intend to spend some time with this. 

Convolutions can be applied in numpy and scipy, the latter providing more options for padding out the edges of the array.

I'm really enjoying the scipy skimage image analysis YouTube demos and exercises to flex those numpy and image filtering muscles. 

**Tomorrows plans:** Try to understand convolution more. Then work through more of the scipy and skimage image analysis video. 

![noise removal](https://github.com/datalass1/100-days-of-code/blob/master/images/day3-filtering-noise-from-arrays.png?raw=true)

### Day 4: 9th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-4-image-filters-smoothing-images.ipynb

**Today's Progress:** Convolution to find the edge in a 1D array. Then running scipy and skimage awesome ready made code/demo to visualise 2D convolution for smoothing imagery by edge detection. I then tried turning my RGB Madagascar tif into a png for easy image reading and manipulation.

**Thoughts:** A day consolidating some of the matplotlib, gdal and skimage.io code. Translating the tif to png was not successful using gdal_translate because of the skewness of pixel values to low DNs. I used skimage's img_as_float to normalise and rescale before exporting in skimage to png. And it worked! 

**Tomorrows plans:** crop the Madagascar image, smooth the image, find edges in the image. 
![edgy](https://github.com/datalass1/100-days-of-code/blob/master/images/day4-finding-edges.png?raw=true)

### Day 5: 10th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-5-Gaussian-filter-smoothing.ipynb

**Today's Progress:** How smooth is Gaussian? Testing smoothing on imagery following the scipy and skimage tutorials. Mean vs. Gaussian and visualisation of the Gaussian curve. Using scipy ndimage again for convolution, skimages img_as_float, and lot's of matplotlib.

**Thoughts:** The only thing that I don't like is that matplotlib won't autocomplete or provide function options when I Shift + Tab. Tip: skimages io function callig io.imshow(image) is useful for quick visualisation of an image. 

**Tomorrows plans:** There are so many options. I need to finish this scipy and skimage tutorial. I would also like to crop my Madagascar image, smooth and find edges. #realsatellitedata

![gaussian](https://github.com/datalass1/100-days-of-code/blob/master/images/day5-gaussian-smoothing.png?raw=true)

### Day 6: 11th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-6-Gaussian-smooth-and-crop-Toliara-barrier-reef.ipynb

**Today's Progress:** Cropped using numpy array slicing and smoothing using Gaussian filter from skimage. 

**Thoughts:** I had to set img_as_float again and there is some interesting info here about sensible rescaling: http://scikit-image.org/docs/dev/user_guide/data_types.html and to reiterate from the lessons so far we use smoothing to reduce noise and pixelation. 

**Tomorrows plans:** practice finding edges and apply it to the Madagascar image.

![toliara reef](https://github.com/datalass1/100-days-of-code/blob/master/images/day6-smooth-toliara-reef.png?raw=true)
