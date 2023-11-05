# PS1-IIRS-Flood-Analysis (Group Project)

This project makes use of Google Earth Engine to acquire and process Sentinel-1 Synthetic Aperture Radar (SAR) data to characterize the 
spatio-temporal patterns of floods in the Assam Valley.

There are typically 4 types of data - optical, microwave, thermal and hyperspectral. Microwave data is what we use as it is better suited for the rainy season.
We monitored rainfall’s impact on Brahmaputra’s water spread by looking at images from
May to October. Water being smooth means the radiation reflects away, and these spaces look
dark. Using this data, we analyzed the spread of river vs rainfall depth.


# Filtering Bands and Polarizations

Sentinel 1 can receive specific polarizations simultaneously and send signals in horizontal or
vertical polarization → HH, HV, VV, VH. It has three different operational modes, which are:
1. Interferometric Wide swath: majorly used

2. Extra wide swath: low resolution but wide

3. Strip map: high resolution but small regions

We got RGB composite from VV, VH, and VV/VH.
We selected images from before and after every month and used the VH band for urban flood
detection, then applied a speckle filter as mentioned in the UN-SPIDER Documentation. Then we
calculated the difference and applied filters to remove pre-existing water, isolated pixels, and steep
because these also can lead to dark spots, and then we calculated the area for the same.


We have found a feature collection for separating the Assam region and also filtered the Sentinel
1 collection using the properties we need, which include the following:
1. Instrument Mode: IW
2. Transmitter Receiver Polarisation: VH
3. Orbit Properties Pass: DESCENDING. We can choose ASCENDING also, but it has to be
anyone because otherwise, it’ll lead to pictures with multiple angles
