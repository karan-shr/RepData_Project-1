# Reproducible Research: Peer Assessment 1
Karan Sharma  
`r Sys.Date()`  

The following documents explains the data analysis undertaken as a part of the Reproducible Research Course in the Coursera-JHU Data Science Specialization. 

## Setup

In this section we setup R working environment by loading the required libraries. 


```r
library(data.table)
library(ggplot2)
```




## Loading and preprocessing the data

The provided data is in zipped, so firstly the data is unzipped. The resulting file is in CSV format and is titled *activity.csv*.

This file is then read into R and saved as a data frame titled *indata*. This data frame is then saved as a data.table object. For this assignment I use data.table library, for more information check data.table [cheat sheet](https://s3.amazonaws.com/assets.datacamp.com/img/blog/data+table+cheat+sheet.pdf).


```r
indata <- read.csv("./activity.csv")
setDT(indata)
```


The first and last five rows of the data are presented in the R output below:


```r
indata
```

```
##        steps       date interval
##     1:    NA 2012-10-01        0
##     2:    NA 2012-10-01        5
##     3:    NA 2012-10-01       10
##     4:    NA 2012-10-01       15
##     5:    NA 2012-10-01       20
##    ---                          
## 17564:    NA 2012-11-30     2335
## 17565:    NA 2012-11-30     2340
## 17566:    NA 2012-11-30     2345
## 17567:    NA 2012-11-30     2350
## 17568:    NA 2012-11-30     2355
```




## What is mean total number of steps taken per day?

1. To calculate the total number to steps taken per day, I use the data.table *by* feature to sum the total number of steps in a day. To ignore the missing values in the assignment, I set *na.rm=TRUE* in the sum function. As a result of this, days where steps were **NA** are treated as days where 0 (zero) steps were recorded. The head and tail of the resulting data.table *steps_perday* are shown in R output below:


```r
steps_perday <- indata[ ,.(total_steps= sum(steps,na.rm = TRUE)), by= date]

head(steps_perday,5)
```

```
##          date total_steps
## 1: 2012-10-01           0
## 2: 2012-10-02         126
## 3: 2012-10-03       11352
## 4: 2012-10-04       12116
## 5: 2012-10-05       13294
```

```r
tail(steps_perday,5)
```

```
##          date total_steps
## 1: 2012-11-26       11162
## 2: 2012-11-27       13646
## 3: 2012-11-28       10183
## 4: 2012-11-29        7047
## 5: 2012-11-30           0
```

\


2. Histogram of the total number of steps taken per day:


```r
hist.steps_perday <- ggplot(data = steps_perday, aes(total_steps)) + 
  geom_histogram(binwidth=2000,colour="red",fill="white")

print(hist.steps_perday)
```

![](PA1_template_files/figure-html/steps/day-hist-1.png) 

\


3. Mean and Median of total number of steps taken per day:

```r
summary.steps_perday <- steps_perday[, .( mean_steps= mean(total_steps, na.rm = TRUE),
                                          median_steps= median(total_steps, na.rm = TRUE))
                                     ]
# Mean of total no. of steps taken per day:
summary.steps_perday$mean_steps
```

```
## [1] 9354.23
```

```r
# Median of total no. of steps taken per day:
summary.steps_perday$median_steps
```

```
## [1] 10395
```
So the **Mean** and **Median** of total no. of steps taken per day are **9354.23** and **10395** respectively.  

\


## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
