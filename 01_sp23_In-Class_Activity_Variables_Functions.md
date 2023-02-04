01_In-Class_Activity-01
================
Naga Vemprala
2023-01-26

## First in-class activity on R objects.

#### Question: 1

``` r
fetch_gender <- function () {
     factor(c("M", "F", "O"), labels = c("Male", "Female", "Other"))
}
gender <- factor(c("M", "F"), labels = c("Male", "Female"))
print("Gender variable before calling function")
```

    ## [1] "Gender variable before calling function"

``` r
print("----------------------------------------")
```

    ## [1] "----------------------------------------"

``` r
print(gender)
```

    ## [1] Female Male  
    ## Levels: Male Female

``` r
print("----------------------------------------")
```

    ## [1] "----------------------------------------"

``` r
print("Gender variable After calling function")
```

    ## [1] "Gender variable After calling function"

``` r
print("----------------------------------------")
```

    ## [1] "----------------------------------------"

``` r
# Call the function fetch_gender and print it 
gender <- fetch_gender()
print(gender)
```

    ## [1] Female Male   Other 
    ## Levels: Male Female Other

#### Question: 2

``` r
# Vector 1 - Create a numeric vector of length 5 with the course ids 101, 255, 355, 461, 491
vector1 <- c (101, 255, 355, 461, 491)
# Vector 2 - Create a character character vector of length 5 and provide the course titles for these 5 courses as, 
# "Software Applications", "Introduction to OTM", "Decision Modeling and Analytics", 
# "R Programming for Business and Analytics", "Intro to Text Analytics".
vector2 <- c("Introduction to OTM", 
             "Decision Modeling and Analytics", 
             "R Programming for Business and Analytics", 
             "Intro to Text Analytics", "Software Applications")
# Vector 3 - Create a first day of class vector (Make sure that this vector is a date vectors)
vector3 <- c("2023-01-16", "2023-01-17", "2023-01-18", "2023-01-16", "2023-01-17")
# Vector 4 - Create a start time vector (Make sure that this vector is a time vectors)
vector4 <- c("2023-01-16 14:10:00", "2023-01-17 17:00:00", "2023-01-18 19:00:00", 
             "2023-01-16 20:35:00", "2023-01-17 18:25:50")
# Include date and time e.g., "2023-01-16 14:10:00", 

# Vector 5 - Create a end time vector (Make sure that this vector is a time vectors)
vector5 <- c("2023-01-16 16:25:00", "2023-01-17 19:10:00", "2023-01-18 20:10:00", 
             "2023-01-16 21:35:00", "2023-01-17 20:25:50")
# Vector 6 - Create a class frequency vector (a numerical vector, 1 represents the class meets once a week, 
# 2 represents the class meets twice a week, etc.)
vector6<- c(1L, 2L, 1L, 1L, 2L)
# Vector 7 - Create a class frequency character vector (R for Thursday, MWF for Monday-Wednesday-Friday class etc)
vector7 <- c("M", "MWF", "TR", "M", "TF")
# Create a data frame using these above vectors
df1 <- data.frame(vector1, vector2, vector3, vector4, vector5, vector6, vector7)
View(df1)
print(df1)
```

    ##   vector1                                  vector2    vector3
    ## 1     101                      Introduction to OTM 2023-01-16
    ## 2     255          Decision Modeling and Analytics 2023-01-17
    ## 3     355 R Programming for Business and Analytics 2023-01-18
    ## 4     461                  Intro to Text Analytics 2023-01-16
    ## 5     491                    Software Applications 2023-01-17
    ##               vector4             vector5 vector6 vector7
    ## 1 2023-01-16 14:10:00 2023-01-16 16:25:00       1       M
    ## 2 2023-01-17 17:00:00 2023-01-17 19:10:00       2     MWF
    ## 3 2023-01-18 19:00:00 2023-01-18 20:10:00       1      TR
    ## 4 2023-01-16 20:35:00 2023-01-16 21:35:00       1       M
    ## 5 2023-01-17 18:25:50 2023-01-17 20:25:50       2      TF

#### Question: 3

``` r
# Create a function to read the first day of class as string and 
# the class frequency to return the next day of the class in the week. 
# Implement switch case instead of a sequence of if-else statements 
next_class <- function (date_as_string, class_frequency){
  next_date <- switch(class_frequency, 
                      "MWF" = as.Date(date_as_string) +2, 
                      "TR" = as.Date(date_as_string) +2,
                      "TF" = as.Date(date_as_string) +3,
                      "M" = as.Date(date_as_string) +7)
  next_date
}
next_class("2023-01-16", "MWF")
```

    ## [1] "2023-01-18"
