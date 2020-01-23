# Lunar Activity
All code used in the analysis of lunar activity patterns and coefficient of overlapping for predators and prey. 

## Overview
### Code Included:

- Lunar Activity Pattern and Overlap Analysis: includes all the code for cleaning, analyzing and plotting data
- Functions Used for Lunar Analysis: all custom background functions used in Lunar Activity Pattern and Overlap Analysis
- Calculating RAO Uniformity for Lunar Activity: runs rao.spacing.test on lunar activity of each species
- Binning Records for Lunar Phase: designates each record by its corresponding lunar phase to calculate the number of records for each species that are within each phase
```
Important Note: Data not included. 
```
Data used in this was data obtained from camera trap photos with date and time recorded. 

Columns needed for this analysis:
  - Species: latin name for species
  - Common: common name for species
  - Time: time of record in decimal format
  - Independent: with designations  as "Yes" for observations of the same species at the same camera within 30 minutes or "No" for non-independent data
  - Longitude: in decimal degrees
  - Latitude: in decimal degrees

## Lunar Activity Pattern and Overlap Analysis
- cleans data 
- calculats lunar phase in radians using getMoonIllmination function from suncalc package (Thierumel & Elmarhraoui, 2019)
- calculates Coefficient of Overlapping and related statistics using overlap package (Meredith & Linkie, 2018)
- builds lunar activity plots 

## Functions Used for Lunar Analysis
- overlapCI*: calculates Coefficient of Overlapping and confidence interval using overlap package (Ridout & Meredith, 2018). Follows the two-step method developed by [Ridout & Linkie (2009)](https://zslpublications.onlinelibrary.wiley.com/doi/full/10.1111/j.1469-7998.2011.00801.x) where sample sizes between 20 and 75 are run with a non-negative trigonometric sum distribution and sample sizes greater than 75 are run with a kernel density with a standard bandwidth of 1 and bandwidth adjustment of 0.8. Uses user-set number of replicates (numboot). In ours we ran it with 10000 replicates. 
- watson2*: calculates U-squared statistics, modified to work with "tied" data (See: Zar, J. H. (1999). Biostatistical analysis. Upper Saddle River, NJ: Prentice Hall)
- watson2test*: approximates p-value of Watson's U-Squared, given two vectors (See: 
 [Tiku, M. L. (1965). Chi-Square approximations for the distributions of goodness-of-fit statistics U2N and W2N. Biometrika, 52. 630-633](https://www.jstor.org/stable/2333714?seq=1). 
 - w.stat*: calculates W statistic from 2 or more vectors of data (in Radians)
 - w.prob*: approximates p-value of W statistic if given 2+ vectors of data (in radians)
 - binning*: function used within chisquare function to bin data into desired number of bins
 - chisquare*: calculates fisher test statistic (determined fisher test was better for general activity pattern analysis as the majority of species vectors did not meet assumptions for chi-square. 
 -plotLunar: activity plots using overlapPlot function from overlap package
 - overall: function that runs all functions above given two vectors of observations to compare
 ```
  * means written by TJ Weigman
  ```
  
 ## Calculating RAO Uniformity for Lunar Activity
  - pvalueRAO: function print.rao.spacing.test altered to save p-value range into data frame (Agostinelli, 2007). From package Circular (2017).
  
  ## Binning Records for Lunar Phase
  - Divides the lunar phase (from 0 to 1 in radians) into 4 equal quadrants centered on each moon phase (First Quarter from pi/4 to 3pi/4, Full Moon 3pi/4 to 5pi/4, Last Quarter 5pi/4 to 7pi/4, and New Moon less than pi/4 or greater than 7pi/4).
  - Each independent record was designated as one of these four phases based on its calculated moon phase
  - Percentage of records in each phase for each species is calculated
 
 ## Authors
 - Amy Eppert (Student in Department of Biology, Point Loma Nazarene University)
 - TJ Weigman (Student in Department of Physics and Engineering, Point Loma Nazarene University)
    - Initial functions for Coefficient of Overlapping and related statistics
