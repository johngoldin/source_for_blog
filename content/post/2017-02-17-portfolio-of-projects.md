---
title: Portfolio of Projects
date: '2017-02-17'
categories:
  - R
  - personal
tags:
  - R
menu: "main"
---
<!--- created with this command:
# blogdown::new_post("Portfolio of Projects", categories = c("R", "personal"), tags = c("R"), rmd = FALSE)  --->
One motivation for creating this blog was to display a portfolio of projects that I have worked
on in the last year or so. I'll list projects here.
The plan is that eventually I will add pages that elaborate each project. I hope that publishing
my projects on this site will nudge me to be a bit more systematic as I execute projects.

### [The Diary of Samuel Pepys](https://goldin.shinyapps.io/Search_Pepys/)

Each morning I read an entry from
[The Diary of Samuel Pepys](http://www.pepysdiary.com/) at a wonderful
site created by [Phil Gyford](http://www.gyford.com/). Pepys kept the diary for about ten years during the 1660's.
Inspired by a post by 
[Julia Silge](http://juliasilge.com/blog/Life-Changing-Magic/), 
I did some simple
text processing on the diary. That became the
occasion for my first shot at creating a Shiny app.
The resulting web page is available [here](https://goldin.shinyapps.io/Search_Pepys/). The code to
create this web page is available on a [GitHub repository](https://github.com/johngoldin/pepys-diary).

I had an opportunity to chat with Julia at the RStudio Conference in Orlando. She gave me some suggestions
for some additional things I might do with the diary.

### [Souvenirs of My Walks](https://goldin.shinyapps.io/Walks/)
<img style="float: right;" src="/img/Lake-District.png", width="158", height="200">I have always loved to walk. When I retired in 2011 I went on a walking binge.
At the same time, I discovered that a GPS trace
could be a fun souvenir of my walks.
An [article](http://mhermans.net/hiking-gpx-r-leaflet.html) I found via [R Bloggers](https://www.r-bloggers.com/) led me
to try to keep track of my walks more systematically.
After doing some research on how to access the Flickr API from R,
I was able to display my photos from Flickr on the GPS trace in a Leaflet map.
The result is a Shiny app [here](https://goldin.shinyapps.io/Walks/).
I don't thnk this is of great interest to a stranger, but for me it is a fascinating
picture of my walks. I love to zoom in and see the detail of the map combined with the GPS trace and the photos.
Like a good souvenir, it triggers lots of memories. If I lingered on a bench additional squiggles appear
on the GPS trace showing where I stopped for a spell. I can also see my wrong turns.
The code for the sourvenir walks site is available at a [GitHub repository](https://github.com/johngoldin/Visualizing-Hiking). There are also some [technical notes]({{< relref "2016-06-28-technical-note-shiny-souvenir-map.md" >}}) and some details on [Flickr from R]({{< relref "2016-07-03-using-the-flickr-api-from-r.md" >}}).

### Connecticut Data by Town
I did somse exploring to see what kind of data I could find and then created some maps via ggplot2 to display some of that data.

### [Census Data](http://rpubs.com/JohnGoldin/196744)
There is an [acs package](http://cran.r-project.org/web/packages/acs/index.html) to access US Census data.
I did a little bit of exploration to see whether I could create maps of New Haven County based on Census data.
Finding the right Census table turned out to be more of a trick than I expected. [Here](http://rpubs.com/JohnGoldin/196744) is a plot of New Haven County published to RPubs.

As I was writing
this summary I found [this blog post](http://www.arilamstein.com/blog/2015/11/16/search-census-data-r/)
that might help. I may get back to that later.

### [An Implementation of Narcissism in R]({{< relref "2017-02-26-narcissism-in-r.html" >}})
Sometimes I just want to play around plotting some data. What data could be more interesting than data about me?
It so happens I have a data series of my daily weight spanning more than 20 years. That's not weird, is it. So I did some charts.

### Jai Alai
Last but not least is jai alai. Back when I was in graduate school, there were two jai alai frontons in Connecticut, Milford and Bridgeport. Actually at one point there was also a third fronton in Hartford.
There are some unique features to the way betting on jai alai is organized that makes it a bit
tricky to analyze. Back then that seemed more interesting than working on my dissertaton. That period of my
life is long past, but the lure of procrastination is still present. So on serveral occasions I have
plunged back into jai alai. Jai alai was one of the first R projects I worked on after I retired. Recently
I spent another month of my life on jai alai.