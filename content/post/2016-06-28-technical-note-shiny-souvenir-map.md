---
title: Technical Note--Shiny Souvenir Map of Walks
date: '2016-06-28'
categories:
  - R
  - Leaflet
  - GPS
  - Flickr
tags:
  - R
---
I have used RStudio’s Shiny to create a [map page](https://goldin.shinyapps.io/Walks/) where I can display GPS traces and photos from walks I have done during the last five years.

The map is based on an example provided by Maarten Hermans in  a [blog post](http://mhermans.net/hiking-gpx-r-leaflet.html) that he published last year. The map uses R htmlwidgets that provide access to the Javascript tool Leaflet. The trick is that I don’t have to know very much about either htmlwidgets or Leaflet to make this work.

Maarten relies on the package rgdal to deal with mapping issues. [GDAL – Geospatial Data Abstraction Library](http://www.gdal.org/) is a [big topic](http://www.osgeo.org/gdal_ogr). I had used it previously to convert map coordinates from the projection used in Great Britain to WGS84, the projection used in the US, Google Earth, and Open Street Maps. Via Maarten’s example I learned that I could use an rgdal function (readOGR) to load in GPS tracks in the GPX format. With a bit of googling I picked up a couple of other useful tools. But I still have the barest understanding of what’s involved with GDAL (and the sp package that relies on rgdal). Back when I was first using rgdal I had some problems properly installing the gdal C libraries on OSX. It took a fair amount of googling to get that sorted out.

The example by Maarten displayed photos from his local server. I wanted to use photos that I had already uploaded to Flickr. There is an API to access Flickr, but at first I had a lot of trouble figuring out how to use it from R. There is an Rflickr package, but it appears to be out of date and no longer functions. Once again googling led me to an [example](http://timelyportfolio.github.io/rCharts_Rflickr/iso_httr.html) that unlocked the technique to use the Flickr API from R. As typically happens, this led me into a couple of other technical byways. I used the package [httr](https://cran.r-project.org/web/packages/httr/index.html) to interact with the Flickr API. Data is returned via JSON. I had heard of that before, but didn’t really understand its purpose. This led me into the package [jsonlite](https://cran.r-project.org/web/packages/jsonlite/vignettes/json-aaquickstart.html). Once I got rolling with the Flickr API I realized that it was very effective and easy to use. Flickr sends me the URL for my pictures and I am able to put that URL into the popup markers that appear on the Leaflet map. The pre-sized photos are only downloaded from Flickr as needed so they popup very quickly.

My camera has a GPS and many of my photos are geo-tagged (depending on whether the camera had enough time to get a GPS fix). But for the camera icons on the GPS trace I did not rely on the GPS info from the camera. Instead I matched the time of the photo with the time of the points on the GPS trace. This works quite well. The GPS records time in universal (i.e. Greenwich) time while the camera generally records the time in the local time zone. I had to adjust for those time difference and sometimes adjust for the fact that in some cases I had the camera set on a wacky time zone.

As always my R code relies on the suite of packages created by [Hadley Wickham](http://priceonomics.com/hadley-wickham-the-man-who-revolutionized-r/). I operate in the Hadleyverse. For this project httr was yet another [hadleyverse](http://adolfoalvarez.cl/the-hitchhikers-guide-to-the-hadleyverse/) package that turned out to do exactly what I needed to do even before I knew I needed it to cope with the Flickr API. (And as an update I will note that we are supposed to refer to the *tidyverse* rather than the *hadleyverse*.)

There are a number tools that put photos on a map with an effect similar to what is displayed here. Flickr has some views that emphasize photos located on maps. If you have a photo that is tagged with longitude and latitude Flickr will show a map view showing other photos in the same location. It is interesting to note that the Flickr map views also rely on the same [Leaflet technology](http://leafletjs.com/) used for this project. (Leaflet is more commonly used with languages other than R.)

I first did a [version of the maps](http://rpubs.com/JohnGoldin/149745) using RMarkdown to publish to the RStudio RPubs site. Fortunately this spring I decided to take the plunge and learn about Shiny. Shiny is a much more natural way to allow me to navigate among the map locations. This is my second Shiny app. (The first was a tool to allow regular expression [search of The Diary of Samuel Pepys](https://goldin.shinyapps.io/Search_Pepys/).) Initially I had a version that worked great on my local machine, but failed when I tried to publish it to the shinyapps.io server. I posted a question to the Shiny Google group and got a helpful response from Joe Chang (the author of Shiny) in under a minute. In my initial version, I created a Leaflet map object and saved it to disk. The Shiny server would then load that object. But it turns out that the Leaflet map object depends on the local file structure so that when I copied that object to the Shiny server it no longer worked. I had to rearrange my code. First I had to assemble the geo-location info from GPS traces and the photo information from Flickr and save that as a data file that I could move to the Shiny server. On the Shiny server I create a Leaflet map and then use that data to add GPS traces and photo markers to the Leaflet map. It takes a noticeable amount of time each time the Shiny app starts up.

See this post for code examples on [how to access Flickr from R]({{< relref "2016-07-03-using-the-flickr-api-from-r.md" >}}).



