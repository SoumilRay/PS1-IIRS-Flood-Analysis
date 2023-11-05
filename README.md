# PS1-IIRS-Flood-Analysis

This project makes use of Google Earth Engine to acquire and process Sentinel-1 Synthetic Aperture Radar (SAR) data to characterize the 
spatio-temporal patterns of floods in the Assam Valley.

There are typically 4 types of data - optical, microwave, thermal and hyperspectral. Microwave data is what we use as it is better suited for the rainy season.
We monitored rainfall’s impact on Brahmaputra’s water spread by looking at images from
May to October. Water being smooth means the radiation reflects away, and these spaces look
dark. Using this data, we analyzed the spread of river vs rainfall depth.


Sentinel 1 can receive specific polarizations simultaneously and send signals in horizontal or
vertical polarization → HH, HV, VV, VH. It has three different operational modes, which are:
1. Interferometric Wide swath: majorly used

2. Extra wide swath: low resolution but wide

3. Strip map: high resolution but small regions

