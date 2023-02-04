01_In-Class_Activity-02
================
Naga Vemprala
2023-01-26

## In-class activity to read files

#### Question: 1

``` r
# Read the csv file into a data frame using read.csv 
# Hint: Check the current path using getwd() 
# Also, unlike working with markdown files, we need to build the complete path for the file in order to read the file. 
# Print the first 6 records of the file read into a data frame. Name the data frame as housingPrices
getwd()
```

    ## [1] "C:/Users/Soha/Documents/Intro_to_r"

``` r
file_name <- paste(getwd(),"/Input/",
    "in_class_melbourne_housing_prices.csv", sep="")

print(file_name)
```

    ## [1] "C:/Users/Soha/Documents/Intro_to_r/Input/in_class_melbourne_housing_prices.csv"

``` r
housingPrices<- read.csv(file_name)
View(housingPrices)
head(housingPrices)
```

    ##       Suburb          Address Rooms Type   Price Method SellerG      Date
    ## 1 Abbotsford     85 Turner St     2    h 1480000      S  Biggin 3/12/2016
    ## 2 Abbotsford  25 Bloomburg St     2    h 1035000      S  Biggin  4/2/2016
    ## 3 Abbotsford     5 Charles St     3    h 1465000     SP  Biggin  4/3/2017
    ## 4 Abbotsford 40 Federation La     3    h  850000     PI  Biggin  4/3/2017
    ## 5 Abbotsford      55a Park St     4    h 1600000     VB  Nelson  4/6/2016
    ## 6 Abbotsford   129 Charles St     2    h  941000      S  Jellis  7/5/2016
    ##   Distance Postcode Bedroom2 Bathroom Car Landsize BuildingArea YearBuilt
    ## 1      2.5     3067        2        1   1      202           NA        NA
    ## 2      2.5     3067        2        1   0      156           79      1900
    ## 3      2.5     3067        3        2   0      134          150      1900
    ## 4      2.5     3067        3        2   1       94           NA        NA
    ## 5      2.5     3067        3        1   2      120          142      2014
    ## 6      2.5     3067        2        1   0      181           NA        NA
    ##   CouncilArea Lattitude Longtitude            Regionname Propertycount
    ## 1       Yarra  -37.7996   144.9984 Northern Metropolitan          4019
    ## 2       Yarra  -37.8079   144.9934 Northern Metropolitan          4019
    ## 3       Yarra  -37.8093   144.9944 Northern Metropolitan          4019
    ## 4       Yarra  -37.7969   144.9969 Northern Metropolitan          4019
    ## 5       Yarra  -37.8072   144.9941 Northern Metropolitan          4019
    ## 6       Yarra  -37.8041   144.9953 Northern Metropolitan          4019

#### Question: 2

``` r
# Print the summary of the housingPrices data set  
summary(housingPrices)
```

    ##     Suburb            Address              Rooms            Type          
    ##  Length:13580       Length:13580       Min.   : 1.000   Length:13580      
    ##  Class :character   Class :character   1st Qu.: 2.000   Class :character  
    ##  Mode  :character   Mode  :character   Median : 3.000   Mode  :character  
    ##                                        Mean   : 2.938                     
    ##                                        3rd Qu.: 3.000                     
    ##                                        Max.   :10.000                     
    ##                                                                           
    ##      Price            Method            SellerG              Date          
    ##  Min.   :  85000   Length:13580       Length:13580       Length:13580      
    ##  1st Qu.: 650000   Class :character   Class :character   Class :character  
    ##  Median : 903000   Mode  :character   Mode  :character   Mode  :character  
    ##  Mean   :1075684                                                           
    ##  3rd Qu.:1330000                                                           
    ##  Max.   :9000000                                                           
    ##                                                                            
    ##     Distance        Postcode       Bedroom2         Bathroom    
    ##  Min.   : 0.00   Min.   :3000   Min.   : 0.000   Min.   :0.000  
    ##  1st Qu.: 6.10   1st Qu.:3044   1st Qu.: 2.000   1st Qu.:1.000  
    ##  Median : 9.20   Median :3084   Median : 3.000   Median :1.000  
    ##  Mean   :10.14   Mean   :3105   Mean   : 2.915   Mean   :1.534  
    ##  3rd Qu.:13.00   3rd Qu.:3148   3rd Qu.: 3.000   3rd Qu.:2.000  
    ##  Max.   :48.10   Max.   :3977   Max.   :20.000   Max.   :8.000  
    ##                                                                 
    ##       Car           Landsize         BuildingArea     YearBuilt   
    ##  Min.   : 0.00   Min.   :     0.0   Min.   :    0   Min.   :1196  
    ##  1st Qu.: 1.00   1st Qu.:   177.0   1st Qu.:   93   1st Qu.:1940  
    ##  Median : 2.00   Median :   440.0   Median :  126   Median :1970  
    ##  Mean   : 1.61   Mean   :   558.4   Mean   :  152   Mean   :1965  
    ##  3rd Qu.: 2.00   3rd Qu.:   651.0   3rd Qu.:  174   3rd Qu.:1999  
    ##  Max.   :10.00   Max.   :433014.0   Max.   :44515   Max.   :2018  
    ##  NA's   :62                         NA's   :6450    NA's   :5375  
    ##  CouncilArea          Lattitude        Longtitude     Regionname       
    ##  Length:13580       Min.   :-38.18   Min.   :144.4   Length:13580      
    ##  Class :character   1st Qu.:-37.86   1st Qu.:144.9   Class :character  
    ##  Mode  :character   Median :-37.80   Median :145.0   Mode  :character  
    ##                     Mean   :-37.81   Mean   :145.0                     
    ##                     3rd Qu.:-37.76   3rd Qu.:145.1                     
    ##                     Max.   :-37.41   Max.   :145.5                     
    ##                                                                        
    ##  Propertycount  
    ##  Min.   :  249  
    ##  1st Qu.: 4380  
    ##  Median : 6555  
    ##  Mean   : 7454  
    ##  3rd Qu.:10331  
    ##  Max.   :21650  
    ## 

#### Question: 3

``` r
# Print the minimum date of the "Date" column 
typeof(housingPrices$Date)
```

    ## [1] "character"

``` r
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
head(dmy(housingPrices$Date))
```

    ## [1] "2016-12-03" "2016-02-04" "2017-03-04" "2017-03-04" "2016-06-04"
    ## [6] "2016-05-07"

``` r
housingPrices$Date <- dmy(housingPrices$Date)
typeof(housingPrices$Date)
```

    ## [1] "double"

``` r
min(housingPrices$Date)
```

    ## [1] "2016-01-28"

#### Question: 4

``` r
# Create a data set containing only 2 bedroom houses 
# Print the summary of the data set two_bedroom_houses
# Print the average price of the two bedroom houses
filter_condition <- housingPrices$Rooms == 2
two_bedroom_houses<- housingPrices[filter_condition, ]
View(two_bedroom_houses)
mean(two_bedroom_houses$Price)
```

    ## [1] 775081.2
