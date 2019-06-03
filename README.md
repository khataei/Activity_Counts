
<!-- README.md is generated from README.Rmd. Please edit that file -->

<style>
body {
text-align: justify}
</style>

# activityCounts

<!-- badges: start -->

[![Travis build
status](https://travis-ci.org/walkabillylab/activityCounts.svg?branch=master)](https://travis-ci.org/walkabillylab/activityCounts)
<!-- badges: end -->

The goal of activityCounts is to calculate ActiLife counts based on the
raw acceleration data.

## Installation

You can install the development version from
[GitHub](https://github.com/) with:

``` r
#install.packages("devtools")
devtools::install_github("walkabillylab/activityCounts")
```

## How to use

### Import the accelerometer data

Note that your dataset should contain at least three columns. Typically
the first column is the raw accelerometer data in the x-direction and
the second and the third columns are raw accelerometer data in y and
z-directions, respectively. There is sample dataset available with this
package, which you can check the sample data format. To see the sample
dataset run:

``` r
library(activityCounts)
View(sampleXYZ)
```

### Calculate counts

To calculate counts for your data, use the counts() function. Here is an
example of using the counts() function. We use sampleXYZ dataset
included in the package and then call the counts() function. The
sampling frequency of our data is 100Hz, so we need to pass this value
when calling the function counts:

``` r
calculated_output <- counts(data = sampleXYZ, hertz = 100)
```

### Input data format.

activityCounts is flexible, and it can handle different format. However,
to use the function, you need to provide x, y, and z raw data. The rest
of the arguments are optional. The package assumes x, y, and z raw data
are stored in the first, second, and the third columns, respectively. If
the order is different use thex\_axis, y\_axis, and z\_axis to indicated
each column of your input has which one the axes. You can use the hertz
argument to pass the sampling frequency. The default values for sampling
frequency is 30 Hz. If your data contains a column of the time of the
measurements, you can use time\_column argument to indicate your desired
column, otherwise, use the start\_time argument to designate the
starting time of your analysis.<br> If none of these methods are used to
indicate the start time, the current time is considered as the start
time. In this example, the first column has the data for the z-axis, and
the fourth column of the data has the data for x-axis, and the sixth
column contains the data for the y-axis. Therefore, assuming the
sampling frequency is 50 Hz, we call the function like
this:

``` r
calculated_output <- counts(data = your_raw_data, hertz = 50, x_axis = 4, y_axis = 6, z_axis = 1)
```

The default values for x\_axis, y\_axis, and z\_axis are one, two, and
three respectively. So if you don’t specify them, the function assumes
the first column is for the x-axis, the second for the y-axis and the
third is for the z-axis.

In the following example, starting time is given:

``` r
my_start_time <- "2017-08-22 12:30:10"
my_counts <- counts(data = sampleXYZ, hertz = 100, start_time = my_start_time)
```

### Check the results

To verify the accuracy of the calculated counts for this particular
dataset, you can compare them with the provided sampleCounts dataset. It
contains counts calculated by ActiLife software and the counts()
function.

``` r
summary(sampleCounts)
```

To see the package help page run:

``` r
?activityCounts
```
