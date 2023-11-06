# PS1-IIRS-Flood-Analysis (Group Project)

This project makes use of Google Earth Engine to acquire and process Sentinel-1 Synthetic Aperture Radar (SAR) data to characterize the 
spatio-temporal patterns of floods in the Assam Valley.

There are typically 4 types of data - optical, microwave, thermal and hyperspectral. Microwave data is what we use as it is better suited for the rainy season.
We monitor rainfall’s impact on Brahmaputra’s water spread by looking at images from
May to October. Water being smooth means the radiation reflects away, and these spaces look
dark. Using this data, we analyze the spread of river vs rainfall depth.


# Filtering Bands and Polarizations

Sentinel 1 can receive specific polarizations simultaneously and send signals in horizontal or
vertical polarization → HH, HV, VV, VH. It has three different operational modes, which are:
1. Interferometric Wide swath: majorly used

2. Extra wide swath: low resolution but wide

3. Strip map: high resolution but small regions

We get RGB composite from VV and VH.
We select images from before and after every month and use the VH band for urban flood
detection, then apply a speckle filter as mentioned in the UN-SPIDER Documentation. Then we
calculate the difference and apply filters to remove pre-existing water, isolated pixels, and steep
because these also can lead to dark spots, and then we calculate the area for the same.


#  Using Feature Collections
We found a feature collection for separating the Assam region and also filtered the Sentinel
1 collection using the properties we need, which include the following:
1. Instrument Mode: IW
2. Transmitter Receiver Polarisation: VH
3. Orbit Properties Pass: DESCENDING. We can choose ASCENDING also, but it has to be
anyone because otherwise, it will lead to pictures with multiple angles

# Using Mosaics
To analyze the impact of rainfall on a particular region, we employ the mosaic function. This
function enables us to average data for a set of images and generates a single image that represents
the entire set.
We begin by collecting two sets of images: one captured before the rainfall and the other captured
after the rainfall. To ensure consistency in our analysis, we select the months of March through
June as the ”before” period and the months of July through October as the ”after” period.
Next, we use the mosaic function to generate two images: one representing the ”before” period
and the other representing the ”after” period. We then clip these mosaic images to the geometry
we have chosen for analysis, which in this case is the Assam location.
This approach allows us to visualize and compare the two images side by side, providing insights
into the effects of rainfall on the Assam region

#  Speckle Filtering
In the context of satellite imagery acquired in the Synthetic Aperture Radar (SAR) format,
speckles refer to the noise that appears in the images due to the backscattering technique used
to generate them. SAR images are formed by sending out a radar signal towards the Earth’s
surface and measuring the time it takes for the signal to bounce back and return to the sensor.
This process results in the detection of echoes that vary in intensity, which are then used to
create an image of the target area.
Speckle formation occurs as a result of the reflection of radar waves from rough surfaces on
the Earth’s surface. The roughness of the surface causes the radar waves to scatter in multiple
directions, leading to pixel-to-pixel variations in the intensity of the echoes detected by the sensor.
This variation in intensity manifests as a granular pattern, which can obscure the underlying
features of interest in the image.
The presence of speckles in SAR images is a challenge for image analysis and interpretation, as it
reduces the visual clarity and can lead to errors in automated processing and analysis. Various
techniques have been developed to mitigate the effects of speckles in SAR images, including
filtering and despeckling algorithms that aim to reduce the noise while preserving the underlying
features of interest.

#  Calculating Flood Area
The next step in the procedure would be to find the difference between the 2 images, before and
after, respectively. We will use the divide function for the same.
After this, we need to threshold the image using a specific threshold which gives us the flooded
area. But, our work is not done here. If we notice carefully, this will also count permanent water
regions and those regions with very low slopes because of the lack of reflection from these places.
So we need to eliminate these areas before counting our final flooded area
We eliminate permanent water using the GSW feature collection containing permanent water
fields.
We also have to remove the misclassified isolated points, i.e., say we have a point that is water
according to our classification, but if we check the 25 closest points around this point and see
the number of water points and we get less than 8 points as water, then that would mean that
this point is misclassified and should not be counted in the same.
Here we use the Google Earth Engine’s in-built terrain algorithm to select property slope and
eliminate areas with a slope less than five, i.e., the slope threshold in our situation. After all
this processing, we get the feature collection with the flooded area marked as red.
