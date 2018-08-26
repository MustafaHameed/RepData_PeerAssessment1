---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document: 
    keep_md: true
---


## Loading and preprocessing the data
Unzip data to obtain a csv file.

``` r
library("data.table")
library(ggplot2)

fileUrl <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
download.file(fileUrl, destfile = paste0(getwd(), '/repdata%2Fdata%2Factivity.zip'), method = "curl")
unzip("repdata%2Fdata%2Factivity.zip",exdir = "data")
```

``` r
activityDT <- data.table::fread(input = "data/activity.csv")
```



## What is mean total number of steps taken per day?
1.  Calculate the total number of steps taken per day

``` r
Total_Steps <- activityDT[, c(lapply(.SD, sum, na.rm = FALSE)), .SDcols = c("steps"), by = .(date)] 

head(Total_Steps, 10)
```

    ##           date steps
    ##  1: 2012-10-01    NA
    ##  2: 2012-10-02   126
    ##  3: 2012-10-03 11352
    ##  4: 2012-10-04 12116
    ##  5: 2012-10-05 13294
    ##  6: 2012-10-06 15420
    ##  7: 2012-10-07 11015
    ##  8: 2012-10-08    NA
    ##  9: 2012-10-09 12811
    ## 10: 2012-10-10  9900

1.  If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day.

``` r
ggplot(Total_Steps, aes(x = steps)) +
    geom_histogram(fill = "blue", binwidth = 1000) +
    labs(title = "Daily Steps", x = "Steps", y = "Frequency")
```

    ## Warning: Removed 8 rows containing non-finite values (stat_bin).

![](https://github.com/mGalarnyk/datasciencecoursera/blob/master/5_Reproducible_Research/project1/%F0%9D%99%BF%F0%9D%99%B0%F0%9D%9F%B7_%F0%9D%9A%9D%F0%9D%9A%8E%F0%9D%9A%96%F0%9D%9A%99%F0%9D%9A%95%F0%9D%9A%8A%F0%9D%9A%9D%F0%9D%9A%8E_files/figure-markdown_github/unnamed-chunk-4-1.png)

1.  Calculate and report the mean and median of the total number of steps taken per day

``` r
Total_Steps[, .(Mean_Steps = mean(steps, na.rm = TRUE), Median_Steps = median(steps, na.rm = TRUE))]
```

    ##    Mean_Steps Median_Steps
    ## 1:   10766.19        10765


## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
