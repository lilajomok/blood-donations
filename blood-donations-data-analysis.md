-   [About](#about)
-   [Data](#data)

About
=====

The main goal of this project is to work on and refine data analysis skills. We will be building a model to predict if a blood donor will donate within a given time window.

Data
====

The provided datasets, `trainingData.csv` and `testData.csv` contains the following variables:

-   `Months since Last Donation`: Number of months since the donor's most recent blood donation.
-   `Number of Donations`: Total number of donations the donor has made.
-   `Total Volume Donated`: Total amount of blood the donor has donated in cubic centimeters.
-   `Months since First Donation`: Number of months since the donor's first blood donation.
-   `Made Donation in March 2007`: The explanatory variable or result - `1` if they donated blood, `0` if they did not donate blood in March 2007.

We can view the first couple of observations of the datasets below:

``` r
# Set working directory
getwd()
```

    ## [1] "/home/lila/Documents/Projects/blood-donations"

``` r
# Import datasets; adjust if datasets are in a different directory
testData = read.csv("data/testData.csv", header = TRUE)
trainingData = read.csv("data/trainingData.csv", header = TRUE)

# Display first rows of datasets
head(trainingData)
```

    ##     X Months.since.Last.Donation Number.of.Donations
    ## 1 619                          2                  50
    ## 2 664                          0                  13
    ## 3 441                          1                  16
    ## 4 160                          2                  20
    ## 5 358                          1                  24
    ## 6 335                          4                   4
    ##   Total.Volume.Donated..c.c.. Months.since.First.Donation
    ## 1                       12500                          98
    ## 2                        3250                          28
    ## 3                        4000                          35
    ## 4                        5000                          45
    ## 5                        6000                          77
    ## 6                        1000                           4
    ##   Made.Donation.in.March.2007
    ## 1                           1
    ## 2                           1
    ## 3                           1
    ## 4                           1
    ## 5                           0
    ## 6                           0

``` r
head(testData)
```

    ##     X Months.since.Last.Donation Number.of.Donations
    ## 1 659                          2                  12
    ## 2 276                         21                   7
    ## 3 263                          4                   1
    ## 4 303                         11                  11
    ## 5  83                          4                  12
    ## 6 500                          3                  21
    ##   Total.Volume.Donated..c.c.. Months.since.First.Donation
    ## 1                        3000                          52
    ## 2                        1750                          38
    ## 3                         250                           4
    ## 4                        2750                          38
    ## 5                        3000                          34
    ## 6                        5250                          42

Since `testData` is our testing data set, it does not have `Made Donation in March 2007` variable.

To make the data analysis a bit efficient, we will rename the variables:

``` r
# Rename variables in testData
colnames(testData)[1] <- "ID"
colnames(testData)[2] <- "monthsLastDonation"
colnames(testData)[3] <- "numDonations"
colnames(testData)[4] <- "totalVolumeDonated"
colnames(testData)[5] <- "monthsFirstDonation"

# Rename variables in trainingData
colnames(trainingData)[1] <- "ID"
colnames(trainingData)[2] <- "monthsLastDonation"
colnames(trainingData)[3] <- "numDonations"
colnames(trainingData)[4] <- "totalVolumeDonated"
colnames(trainingData)[5] <- "monthsFirstDonation"
colnames(trainingData)[6] <- "madeDonation"

# Display first rows of datasets
head(trainingData)
```

    ##    ID monthsLastDonation numDonations totalVolumeDonated
    ## 1 619                  2           50              12500
    ## 2 664                  0           13               3250
    ## 3 441                  1           16               4000
    ## 4 160                  2           20               5000
    ## 5 358                  1           24               6000
    ## 6 335                  4            4               1000
    ##   monthsFirstDonation madeDonation
    ## 1                  98            1
    ## 2                  28            1
    ## 3                  35            1
    ## 4                  45            1
    ## 5                  77            0
    ## 6                   4            0

``` r
head(testData)
```

    ##    ID monthsLastDonation numDonations totalVolumeDonated
    ## 1 659                  2           12               3000
    ## 2 276                 21            7               1750
    ## 3 263                  4            1                250
    ## 4 303                 11           11               2750
    ## 5  83                  4           12               3000
    ## 6 500                  3           21               5250
    ##   monthsFirstDonation
    ## 1                  52
    ## 2                  38
    ## 3                   4
    ## 4                  38
    ## 5                  34
    ## 6                  42
