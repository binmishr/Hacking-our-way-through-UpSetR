# Hacking-our-way-through-UpSetR

The details of the codeset and plots are included in the attached Microsoft Word Document (.docx) file in this repository. 
You need to view the file in "Read Mode" to see the contents properly after downloading the same.

The UpsetR package is attached with this repository as .ZIP file.

UpsetR Package - A Brief Introduction
======================================

UpSetR generates static UpSet plots. The UpSet technique visualizes set intersections in a matrix layout and introduces aggregates based on groupings and queries. The matrix layout enables the effective representation of associated data, such as the number of elements in the aggregates and intersections, as well as additional summary statistics derived from subset or element attributes.A Python package called py-upset to create UpSet plots has been created by GitHub user ImSoErgodic.

Sample Data
============
Sample data sets for UpSetR are included in the package and can be loaded like this:

    movies <- read.csv( system.file("extdata", "movies.csv", package = "UpSetR"), header=T, sep=";" )
    mutations <- read.csv( system.file("extdata", "mutations.csv", package = "UpSetR"), header=T, sep = ",")

The movie data set created by the GroupLens Lab and curated by Bilal Alsallakh and the mutations data set was originally created by the TCGA Consortium and represents mutations for the 100 most mutated genes in a glioblastoma multiforme cohort.

Examples
==========

There are currently four vignettes that explain how to use the features included in the UpSetR package:

    Basic Usage
    Queries
    Attribute Plots
    Set Metadata

Demo
=====
A view of the UpSet plot with additional plots based on elements in the intersections.

![image](https://user-images.githubusercontent.com/26252963/149611309-5637fc8f-d209-4866-9610-430980810244.png)


    upset(movies,attribute.plots=list(gridrows=60,plots=list(list(plot=scatter_plot, x="ReleaseDate", y="AvgRating"),
    list(plot=scatter_plot, x="ReleaseDate", y="Watches"),list(plot=scatter_plot, x="Watches", y="AvgRating"),
    list(plot=histogram, x="ReleaseDate")), ncols = 2))

image
======
upset(mutations, sets = c("PTEN", "TP53", "EGFR", "PIK3R1", "RB1"), sets.bar.color = "#56B4E9",
order.by = "freq", empty.intersections = "on")

An example using two set queries (war movies and noir movies) along with attribute plots comparing the average rating (top) and average rating vs the number of times the movies have been watched (bottom).


![image](https://user-images.githubusercontent.com/26252963/149611339-327841f7-7010-46f5-9599-278b0540ecab.png)

    upset(movies, attribute.plots=list(gridrows = 100, ncols = 1, 
    plots = list(list(plot=histogram, x="AvgRating",queries=T),
    list(plot = scatter_plot, y = "AvgRating", x = "Watches", queries = T))), 
    sets = c("Action", "Adventure", "Children", "War", "Noir"),
    queries = list(list(query = intersects, params = list("War"), active = T),
    list(query = intersects, params = list("Noir"))))

Download
=========
Install the latest released version from CRAN

install.packages("UpSetR")
