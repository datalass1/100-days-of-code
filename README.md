# I've joined the #100DaysOfCode Challenge

### Day 0: 5th April
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

### Day 7: 13th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-7-downloading-amazon-imagery-with-sentinelsat-GDAL.ipynb

**Today's Progress:** Downloading imagery again, this time looking over the Amazon rainforest at a place called Amapa which has a high level of deforestation. Once again using sentinelsat and gdal. Trying out rasterio for visualisation.

**Thoughts:** Ran out of time to perfect visualisation, working on this for about 4hours. Time flies when gathering data and trying to formulate some sort of plan for a project. I did a bit of a turn on my plans and instead of Madagascar I am looking at the Amazon rainforest, it will be easier to segment and find edges forest or not forest.

**Tomorrows plans:** Continue with the plans to visualise and try smoothing and segmentation of the imagery. I could test with skimage data first and the try on the satellite imagery. 

### Day 8: 14th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-8-and-9-working-with-rasterio-amazon-cropping.ipynb

**Today's Progress:** continued work with satellite imagery. I find that working with rasterio might be a better choice than skimage for geospatial imagery. skimage has some cool functionality that I could call on for edge detection and segmentation but for reading data in and out rasterio may be the better option. New packages I worked with today: Shapely, GeoPandas and Pycrs. 

**Thoughts:** Changing tack is difficult. I didn't finish today with a beautifully polished script or visualisations. But I did learn about reading data in and out, perhaps skimage will be usful for general image manipulation but reading in and out I need gdal or rasterio. I tried cropping my Amazon image, it ended up in the wrong location, I need to understand affine and transform more.

**Tomorrows plans:** Figure out how to put my cropped image in the correct location! Then start smoothing and image manipulation if there is time tomorrow. 

### Day 9: 15th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-8-and-9-working-with-rasterio-amazon-cropping.ipynb

**Today's Progress:** Successful work with rasterio, I fixed the affine problem. It was down to a spelling error...classic! But along the way I found a great book to read and understand more: Geoprocessing with Python by Chris Garrard. 

**Thoughts:** It is strange that the values of the 2016 and 2018 imagery differ so much...perhaps something to investigate further. Shame to see so much cloud cover in 2016 as well, but not surprising over the Amazon rainforest (not dryforest).

**Tomorrows plans:** Read more of Chris Garrards chapter on raster geoprocessing and do some further EDA on the imagery then if there is time some Gaussian smoothing and perhaps further image analysis. 

![2016](https://github.com/datalass1/100-days-of-code/blob/master/images/day9-2016-DNs.png?raw=true)
![2018](https://github.com/datalass1/100-days-of-code/blob/master/images/day9-2018-DNs.png?raw=true)

### Day 10: 16th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-10-ndvi-over-amazon-rainforest-amapa-chip.ipynb

**Today's Progress:** Calculating NDVI for the Amazon rainforest crop over Amapa, Brazil. Healthy vegetation reflects NIR more, think of a False colour image. Playing about with matplotlib to create subplots of two plots with one colorbar. 

**Thoughts:** Rasterio will open the tif as a `numpy array` when using `with rasterio.open(image_path) as src: image = src.read()` whereas by opening the tif as `image = rasterio.open(image_path)` creates an object type for reading: `rasterio._io.RasterReader`. By using a with statement ensures that files are closed.

**Tomorrows plans:** Read more of Chris Garrards chapter on raster geoprocessing, don't give up, what other work can you do with image processing over the Amazon? Is there more statistical analysis of pixel counts, visulaisation (such as histograms) and image manipulation :)

![ndvi](https://github.com/datalass1/100-days-of-code/blob/master/images/day10-ndvi-amazon-rainforest-amapa.png?raw=true)

### Day 11: 17th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-11-CoNVO-mapping-amazon-rainforest-river-system.ipynb

**Today's Progress:** SO! I did not want to go back to Gaussian smoothing when I had already successfully tested it on the Toliara coral reef imagery. I spoke with Tom at work about my lack of direction and interest in mapping the Amazon and he suggested I write a CoNVO. This stands for Context, Need, Vision and Outcome.

**Thoughts:** The why before the how. Finding the data and the technicques with machine learning to fit to the problem rather than finding a problem to fit to the data. So in Day 11's notebook you will find my CoNVO. I used Thinking with Data by Max Shron book to get the basics. Having vision is difficult and is dependent on experience, and there is no shortcut to experience, I particularly liked this quote: 

*"There is a saying in the world of Go: lose your first fifty games of Go as quickly as possible."*

Quality comes with experience. So forgive me if my CoNVO is nonsense, some of it actually it (i.e. I made it up). 

**Tomorrows plans:** Get started on this awesome project. 

### Day 12: 19th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-12-and-13-kanban-prep-and-k-means-testing.ipynb

**Today's Progress:** Busy day working on kanban. Lot's of research trying to find the best machine learning techniques for classification to apply to satellite imagery. Tested k-means from scikit learns cluster module. 

**Thoughts:** A great first machine learning technique to try. A nice beginners algorithm that will find patterns in data to create a model. I used the clustering on the blue band of the TCI JP2 from Sentinel. Git problems today, corrupt with object file error and fsck segementation fault. After trying to fix for 1hr I cloned from remote repo again and moved the new ipynbs from a copy of the local repo. It worked (yay!) and the only thing I have lost is my .git history (that i know of so far). 

**Tomorrows plans:** Continue refining the k-means and kanban. 

### Day 13: 20th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-12-and-13-kanban-prep-and-k-means-testing.ipynb

**Today's Progress:** A great short session finishing off yesterday work on k-means. Perfecting the affine to output the tif with the correct origin for spatial reference. 

**Thoughts:** Happy that affine worked. Again, thanks to Geoprocessing with Python by Chris Garrard. K-means not great, water pixels mixed up with forest etc and the smalled rivers classifed seperately to the larger rivers. 

**Tomorrows plans:** Kanban and next steps. knn could be worth looking into at this stage for some OBIA, is it OBIA...hmm?

![kmeans](https://github.com/datalass1/100-days-of-code/blob/master/images/day13-kmeans.png?raw=true)

**Additional note:** A [twitter thread recommended by Sean Gillies](https://twitter.com/sgillies/status/1119738614169001984) on affine/geotransform differences between gdal, ESRI world file and rasterio. Also in the thread is a link to tHE tissot indicatrix. 

### Day 14: 21st April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-14-ndwi-k-means-amazon.ipynb

**Today's Progress:** trying ndwi with k-means. Better results than I had with just k-means on one band. 

**Thoughts:** A full ipynb created to collect imagery from sentinel hub, extract jp2s of bands 1,2,3 and 8 to tifs, create a false color learnt from Chris Garrards Geoprocessing book chpt 9, then ndwi and k-means with sklearn cluster. Great result. 

**Tomorrows plans:** Some visualisation of this result.

![nwdi k-means](https://github.com/datalass1/100-days-of-code/blob/master/images/day14-ndwi-k-means.png?raw=true)

**Revisit:** Use k-means on ALL the satellite bands, a useful [tutorial](https://www.linkedin.com/pulse/k-means-python-3-sentinel-2-data-andrew-cutts). Also, how do we understand optimum number of clusters for dataset? [This tutorial](https://learning.oreilly.com/learning-paths/learning-path-machine/9781838820725/9781789340525-video2_2) on compactness score and expectations from k-means.

### Day 15: 22nd April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-15-and-16-visualising-and-polygonizing-river-data.ipynb

**Today's Progress:** Started with numpy where `np.where` statement to change all non-river values to NaN. Then tried some visualisation with folium for raster and potentialy vector data. 

**Thoughts:** using gdal_polygonize.py for raster to polygon. It did not like NaN values. Folium was also struggling to show ImageAsOverlay with the reprojected raster. Raster reprojected using rasterio, really handy script found online, link in notebook. 

**Tomorrows plans:** Continue with visualisation and polygonization. 

### Day 16: 23rd April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-15-and-16-visualising-and-polygonizing-river-data.ipynb

**Today's Progress:** Failure with folium, success with polygonisation.

**Thoughts:** Backed out of the interesting folium rabbit hole, and decided that unless I am in need of a webmap I could be quite happy with QGIS and matplotlib for visualisation ... so I included a histogram today and a terrain cmap, as well as the image below snapped from QGIS. The reprojected to web mercator tif for foliums ImageOverlay was showing up in the correct location but as a grey box. gdal polygonize.py worked today, I changed nothing compared to yesterday. 

**Tomorrows plans:** Move onto more machine learning.

![rivers](https://github.com/datalass1/100-days-of-code/blob/master/images/day15-rivers-overlay-false-color-tif.png?raw=true)

### Day 17: 24th April
**Today's Progress:** Feeling a bit run-down today I committed to the 100 Days of Code challenge by downloading Francois Chollet (author of Keras) audio book 'Deep Learning with Python', here it is on [oreilly](https://learning.oreilly.com/library/view/deep-learning-with/9781617294433/kindle_split_000.html).

**Thoughts:** The book starts with some of the history. Ada Lovelace in the 1850s commenting on the analytical machine. Alan Turing 100years later questioning whether general purpose computers could generate orginality e.g. the Turing Test. Definitions, such as Machine Learning is "searching for useful representations of some input data, within a pre-defined space of possibilities, using guidance from a feedback signal." And other tecnical terms, weights, loss functions, probablistic modelling (naive bayes and logistic regression), neural networks, backpropagation.  

**Tomorrows plans:** Either back to machine learning or the audio book again. 

### Day 18: 27th April

**Today's Progress:** Started looking at Hands-on Machine Learning with Scikit-Learn, Keras, and TensorFlow, 2nd Edition
by Aurélien Géron to get acquinted with scikit-learn to train myself up so I can apply Random Forest to the satellite image. I created a day-future nb for random forest and got the S2 data prepped.  

**Thoughts:** Knowing where to start; reading, tutorials, blogs. #CantSeeTheWoodForTheTrees

**Tomorrows plans:** Try a random forest tutorial for imagery, and answer how and why it will be useful for mapping rivers in the amazon. 

### Day 19: 28th April
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-19-exploring-random-forest.ipynb

**Today's Progress:** Further research on ensemble methods and Random Forest Classifier, with testing on the iris and breast cancer sklearn datasets.

**Thoughts:** Starting with deicion trees in Scikit-Learn that uses the Classification And Regression Tree (CART) algorithm. This is a binary (yes/no), greedy algorithm which looks for optimum split reducing cost (called recursive binary splitting). To avoid overfitting use regulaization e.g. restrict the maximum depth of the decision tree. 

Ensemble methods are meta-algorithms that combine several machine learning techniques into one predictive model in order to decrease variance (bagging), bias (boosting), or improve predictions (stacking). I looked into combining Bagging classifier and KNN for better results on the sklearns breast cancer dataset.  

Random Forest is an extension of bagged (bootstrap aggregating) decision trees. Each tree in the ensemble is built from a sample drawn with replacement (bootstrap) and instead of using all features, a random subset of feature is selected, further randomising the tree. 

Boosting is useful for convert weak learners to strong learners. 

[This is a great blog post](https://blog.statsbot.co/ensemble-learning-d1dcd548e936) on the subject of today.

"This is how you win ML competitions: you take other peoples’ work and ensemble them together.” Vitaly Kuznetsov NIPS2014

**Tomorrows plans:** Contiue looking at ensemble methods and Randon Forest for classification of imagery. 

### Day 20: 29th April

**Today's Progress:** Watched some awesome Google Earth Engine API tutorials on Arrays and Classification. 

**Thoughts:** Top Tip is to always watch these videos sped up, sometimes 2x speed (especially if it is a workshop). Links to the great tutorials to code from: 
- [Classification with Noel Goerlick]( https://developers.google.com/earth-engine/classification)
- [Some tutorial notes for GeoHacWeek2018](https://docs.google.com/document/d/1keJGLN-j5H5B-kQXdwy0ryx6E8j2D9KZVEUD-v9evys/edit#)
- [My Classification code](https://code.earthengine.google.com/84027208bf2a94e77b5f14075fc5a938)

**Tomorrows plans:** Get on and try out some of the classification models in GEE. 

### Day 21: 30th April
Link to GEE script: https://code.earthengine.google.com/8647c08ceae6f8a300f47a2bcda862fc

**Today's Progress:** Created a GEE javaScript for image classification using the CART algorithm, started looking at an accuracy test using confusion matrix. 

**Thoughts:** Great fun using GEE for image classification workflow training. Spoke with Tom today in pursuit of my interest in Object Based Image Analysis and he suggests image segementation that I can pick up from the skimage library. I previously looked at this technique in the video I watched in days 1-6 but I didn't apply segmentation, now I have a good reason! 

GEE top tip: the help button in top right provides a list of keyboard shortcuts. 

A really helpful [post on calculating fallow land in California with RF](https://github.com/brmagnuson/LandFallowingInEarthEngine).

**Tomorrows plans:** Aim to complete GEE work then move onto image segmentation and ML in python with skimage and sklearn. So tomorrow work on Random Forest and accuracy assessment. 

### Day 22: 1st May
Link to GEE Script: https://code.earthengine.google.com/6a0779085f023dab360325a649cf8c9e

**Today's Progress:** Back in GEE trying Random Forest and cloud removal using a cirrus and cloud mask from the Sentinel-2 Q60 band and then creating a single image using median pixel values. I also tried to be smart with the training data.

**Thoughts:** Trying to be smart with the training data and use the water mask pixels from MODIS/006/MOD44W as locations for training data. Similar example used in the 20190430-RF-classifier-example javascript Random Forest example. 

**Tomorrows plans:** Have a look at training data options, finish Random Forest. 

### Day 23: 5th May
Link to GEE Script: https://code.earthengine.google.com/7ad725eb9a5f699a6315ae2e28ab43ee

**Today's Progress:** Finished up Google Earth Engine work after completing a Random Forest with accuracy assessment confusion matrix. 

**Thoughts:** Accuracy 98% with false positives of water: over-predicting. With such a small subset of data point for training and testing the result is rather salt and peppery. I think the k-means looked better!

**Tomorrows plans:** Ready to move onto some python code and libraries for random forest.

### Day 24: 6th May
Link to notebook: https://github.com/datalass1/100-days-of-code/blob/master/notebooks/Day-24-image-segmentation-with-skimage-examples.ipynb

**Today's Progress:** Great experience using scikit-image and numpy for math to perform image segmentation. Today I tested thresholding for image segmentation on text and supervised segementation with active contour and random walker. 

**Thoughts:** The math to create a circle was a good learning point for revising some high school trigonometry. 

**Tomorrows plans:** More image segmentation and practice. 

### Day 25 and 26 May

**Today's Progress:** On these days I am listening to Fracois Chollets audiobook Deep Learning with Python and working through sololearn to refine my python coding. 

**Thoughts:** A useful way to learn when working through a sprint at work; 9 hour days and lots of interesting work. 

**Tomorrows plans:** I would like to pick up where I left off and go back to image segmentation and practice.

### Day 27: 11th May

**Today's Progress:** It is really challenging to maintain consistency and habitat. This past few weeks in a sprint at work to map mangroves using Sentinel 2 imagery has been really interesting but maxed me out. I'm also aware that I need to work on my development to Data Scientist. So in the spirit of mixing thing up a bit I've decided to do a Kaggle Playground challenge. Today I tackled the Titanic predictions dataset. It is a really great dataset to get started on Kaggle with and so I have focussed today on Exploratory data analysis aka EDA and visualisation using matplotlib and seaborn. 

**Thoughts:** Visualisation is fun, and enjoying using Pandas so much too. 

**Tomorrows plans:** Get into the Machine Learning bit. 

### Day 28: 12th May

**Today's Progress:** Today I completed work on NaNs, grouping data into categories, a few more visualisations and researching the data prep required for machine learning: label, binary and one-hot encoding.  

**Thoughts:** I used pandas `apply` with a lambda function, pandas `map` with a dictionary of new values and pandas `groupby`

**Tomorrows plans:** Continue machine learning research and get started. 

### Day 29: 13th May

**Today's Progress:** Today I researched and completed encoding as part of feature engineering. 

**Thoughts:** I had to understand whether I should use label (ordinal), binary, one-hot, dummy to transform categorical data into numerical data. I used `pandas.get_dummies` following the advice in [Hands-on Machine Learning with Scikit-Learn, Keras, and TensorFlow, 2nd Edition Chpt 2, by Aurélien Géron ](https://learning.oreilly.com/library/view/hands-on-machine-learning/9781492032632/ch02.html). I dropped the unnessary column, remember `axis` argument. 

**Tomorrows plans:** Try out the machine learning classifiers - logistic regression, random forest and others. What gets the best result and how to I calculate the accuracy. 

### Day 30, 31 and 32: 14th to 16th May

**Today's Progress:** Working through Deep Learning with Python by Francois Chollet on audiobook and [o'reilly video edition](https://learning.oreilly.com/videos/deep-learning-with/9781617294433VE/9781617294433VE-DLwP_Chapter2Section4)

**Thoughts:** Looking at tensor dimensions and operations with emphasis on code rather than equations.

**Tomorrows plans:** Get back to ensemble learning. 

### Day 33: 18th May

**Today's Progress:** Back to titanic and looking at a logisitic regression model.

**Thoughts:** Learning about sigmoid acitivation model evaluation.

**Tomorrows plans:** finish code with happy understanding of what is going on. 

### Day 34 and 35: 19th and 20th May

**Today's Progress:** Working through Deep Learning with Python.

**Thoughts:** Learning about Tensor operations such as Tensor re-shaping with `np.reshape` or `np.transpose` (to switch columns and rows). Tensor dot with `np.dot`. The a neural network is avery complex geometric transformation in a high dimensional space, implemented via a long series of simple steps. 

Gradient based optimization works on the fact that all operations in the network are **differentiable**. 

First step: calcualte the relu `output = relu(dot(W, input) + b)` then calculate loss to update the weights efficiently with gradient based optimization. 

**Tomorrows plans:** Back to Titanic. 

### Day 36: 21st May

**Today's Progress:** Back to logistic regression for the titanic kaggle competition. 

**Thoughts:** Learning that it is important to scale numerical data. Using scikit-learn `StandardScalar()`.

**Tomorrows plans:** Continue with logisitic regression classifier. 

## Day 37: 22nd May

**Today's Progress:** Finished logistic regression using `sklearn.linear_model LogisticRegresion()`. I made sure that I used `sklearn.model_selection train_test_split` to create a 20% of the training data for validation. The test dataset from Kaggle is not labelled. My accuracy: 84% on the train set and 79% on the validation. Indicates slight overfitting. 

**Thoughts:** So many other notebooks and blogs make logistic regression seem so complicated...until I found [Mashimo's blog](https://mashimo.wordpress.com/2018/03/31/logistic-regression-using-sklearn/). I also found chpt 2 on end-to-end machine learning in [Hands-on Machine Learning with Scikit-Learn, Keras, and TensorFlow, 2nd Edition by Aurélien Géron](https://learning.oreilly.com/library/view/hands-on-machine-learning/9781492032632/ch02.html#) useful. I really liked the use of `sklearn.pipeline`.

I used `intercept_` and `coef_` to view the model weights and bias. 

**Tomorrows plans:** Look at Random Forest to see if I get a better result. 

## Day 38, 39 and 40

**Today's Progress:** Getting a deeper understanding of Logistic Regression before moving onto Random Forest. 

**Thoughts:** Enjoying the [ML-cheatsheet](https://ml-cheatsheet.readthedocs.io/en/latest/logistic_regression.html) and [Andrew Ng's coursera course on Machine Learning](https://www.coursera.org/learn/machine-learning/home/welcome). Good blog on [linear regression](https://towardsdatascience.com/linear-regression-cost-function-gradient-descent-normal-equations-1d2a6c878e2c) and week 3 of the [ML course](https://medium.com/@rgotesman1/learning-machine-learning-part-3-logistic-regression-94db47a94ea3)

**Tomorrows plans:** Finish logsitic regression and code for it on the Titanic dataset. 


## Day

**Today's Progress:**

**Thoughts:**

**Tomorrows plans:** 


# Glossary of Data Science Terminology

**Machine Learning**
[Machine Learning is the] field of study that gives computers the ability to learn without being explicitly programmed, Arthur Samuel, 1959. And a more engineering-oriented one: A computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E, Tom Mitchell, 1997

Source: Hands-on Machine Learning with Scikit-Learn, Keras, and TensorFlow, 2nd Edition by Aurélien Géron

# Backlog

**Python API in QGIS** suggested by Cate.

**Creating quality images for using visualisation automation of satellite imagery:** check out the [BBC Earth from Space](https://www.bbc.co.uk/iplayer/episode/p072n7qd/earth-from-space-series-1-1-a-new-perspective) for the beautiful imagery and seamless transitions from various imaging platforms suggested by Austin.

**Visualisation with PyViz:** [tutorial](http://pyviz.org/tutorial/index.html) and [video](https://www.youtube.com/watch?v=k27MJJLJNT4), about [holoviews](http://holoviews.org/), [geoviews](http://geoviews.org/), some cool notebookes: [airports](https://anaconda.org/philippjfr/airport_connections/notebook), [nyc taxi](http://datashader.org/topics/nyc_taxi.html), [OSM points](http://datashader.org/topics/osm-1billion.html). Using dask functionality, here is the [docs](https://docs.dask.org/en/latest/) and a [tutorial](https://github.com/dask/dask-tutorial/) suggested by Andrew.
