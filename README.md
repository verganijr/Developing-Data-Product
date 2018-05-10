---
title: "Earthquakes in different countries over seven-day period in 2012"
author: "Antonio Cesar Vergani Junior"
date: "April 18, 2017"
output:
  html_document:
    df_print: paged
  pdf_document: default
always_allow_html: yes
---

This data source contains data representing seismic events in different countries over a seven-day period in 2012. Earthquake data is collected in real-time by geological institutions worldwide, such as the United States Geological Survey (USGS). You can find further details about the data types on the USGS website.
The data is found in the URL:

http://js.cit.datalens.api.here.com/datasets/starter_pack/Earthquakes_7day.csv.

This work is also available in https://verganijr.github.io/Developing-Data-Product/index.html

## Reading Data

The source data contains 1076 rows: 

```{r, echo=TRUE, results=FALSE}
if(!require(leaflet)){
    install.packages("leaflet")
    library(leaflet)
}

if(!require(htmltools)){
    install.packages("htmltools")
    library(htmltools)
}
data <- "http://js.cit.datalens.api.here.com/datasets/starter_pack/Earthquakes_7day.csv"
df <- read.csv(url(data))
df <- df[sample(nrow(df),), c(5,6)]

```
 
## Plotting Map

The map below shows a clustered view of all the spots where seismic events in different countries over a seven-day period were recorded by geological institutions worldwide in September of 2012: 

```{r Leaflet, echo=TRUE}

df %>%
  leaflet() %>%
  addTiles() %>%
  addMarkers(clusterOptions = markerClusterOptions(), popup = ~htmlEscape(df$Region))

```
