Concentration Index USA 1956–2006
================
Dominic Royé
9 de diciembre de 2018

The contiguous US exhibits a wide variety of precipitation regimes, first, because of the wide range of latitudes and altitudes. The physiographic units with a basic meridional configuration contribute to the differentiation between east and west in the country while generating some large interior continental spaces. The frequency distribution of daily precipitation amounts almost anywhere conforms to a negative exponential distribution, reflecting the fact that there are many small daily totals and few large ones. Positive exponential curves, which plot the cumulative percentages of days with precipitation against the cumulative percentage of the rainfall amounts that they contribute, can be evaluated through the Concentration Index. The Concentration Index has been applied to the contiguous United States using a gridded climate dataset of daily precipitation data, at a resolution of 0.25°, provided by CPC/NOAA/OAR/Earth System Research Laboratory, for the period between 1956 and 2006. At the same time, other rainfall indices and variables such as the annual coefficient of variation, seasonal rainfall regimes and the probabilities of a day with precipitation have been presented with a view to explaining spatial CI patterns. The spatial distribution of the CI in the contiguous United States is geographically consistent, reflecting the principal physiographic and climatic units of the country. Likewise, linear correlations have been established between the CI and geographical factors such as latitude, longitude and altitude. In the latter case the Pearson correlation coefficient (r) between this factor and the CI is −0.51 (p-value &lt; 0.001). For annual probability of days with precipitation and the CI there is also a significant and negative correlation, r = −0.25 (p-value &lt; 0.001).

-   Fig. 8. Concentration Index values (1956–2006).

``` r
library(ggplot2)
library(sf)
```

    ## Linking to GEOS 3.6.1, GDAL 2.2.3, PROJ 4.9.3

``` r
library(raster)
```

    ## Warning: package 'raster' was built under R version 3.5.1

    ## Loading required package: sp

``` r
library(RColorBrewer)

ci_raster.proj <- raster("Data/ci_raster_USA.tif")

limit <- st_read("Data/USA_limit/USA_continental.shp")
```

    ## Reading layer `USA_continental' from data source `C:\Users\xeo19\Documents\GitHub\Concentration_Index_USA\Concentration_Index_USA\Data\USA_limit\USA_continental.shp' using driver `ESRI Shapefile'
    ## Simple feature collection with 1 feature and 13 fields
    ## geometry type:  POLYGON
    ## dimension:      XY
    ## bbox:           xmin: -124.7158 ymin: 25.11555 xmax: -66.96889 ymax: 49.37666
    ## epsg (SRID):    4326
    ## proj4string:    +proj=longlat +datum=WGS84 +no_defs

``` r
ci_raster.proj_df <- as.data.frame(ci_raster.proj,xy=TRUE,na.rm=TRUE)
names(ci_raster.proj_df)[3] <- "CI"

col_ci <- brewer.pal(11,"RdBu")

ggplot()+
    geom_tile(data=ci_raster.proj_df,
            mapping=aes(x,y,fill=CI))+
     geom_sf(data=limit,fill="transparent")+
       scale_fill_gradientn(colours=rev(col_ci))+
       coord_sf(crs=2163,datum=NA)+
      theme_void()
```

![](README_files/figure-markdown_github/unnamed-chunk-1-1.png)

-   Fig. 4. Seasonal rainfall regimes (1956–2006) (P, spring, S, summer, A, autumn, W, winter)

How to cite
-----------

Royé D & Martin-Vide J (2017). Concentration of Daily Precipitation in the Contiguous United States. Atmospheric Research, 196C:237-247, doi: [10.1016/j.atmosres.2017.06.011](https://doi.org/10.1016/j.atmosres.2017.06.011).
