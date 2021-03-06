---
title       : Developing Data Products Week 4
subtitle    : Chicken Weight vs Age Pitch Presentation
author      : Arjan van Vliet
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

* An R Shiny App was created to analyze chicken weight over time for different diets
* Using interactivity it is possible to plot weight development over time in different ways:
    + All individual chickens
    + An average for the different diets
* In both cases the time windows can be adjusted
* The Shiny App is hosted on the free hosting plaform from Shiny: 'shinyapps.io'

---

## Weight increase per diet (code example)

The plot to show the average weight increase for each sample is generated using below code.


```r
library(dplyr)
library(ggplot2)

# input$time_range holds the min and max time values selected using a slider
data <- ChickWeight %>%
    filter(Time >= input$time_range[1] & Time <= input$time_range[2]) %>%
    group_by(Diet, Time) %>%
    summarise(avg_weight = mean(weight))

gg <- ggplot(data)
gg <- gg + geom_line(mapping = aes(x = Time, y = avg_weight, colour = Diet))
gg <- gg + scale_y_continuous(expand = c(0, 0), limits = c(0,300))
gg <- gg + ylab("Average Weight")
gg
```

---

## Weight increase per diet (plot example)

This plot shows the average weitght increase over time for the four different diets with a starting time of 8 days.

<img src="assets/fig/unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />

---

## Thank You

Thanks for viewing this pitch!

Please visit the shiny app and use it:

https://arjanvanvliet.shinyapps.io/DevelopingDataProductsWeek4/
