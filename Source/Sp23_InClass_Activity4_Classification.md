Logistic Regression
================

## Logistic Regression

In statistics, the logistic model (or logit model) is used to model the
probability of a certain class or event existing such as pass/fail,
win/lose, alive/dead or healthy/sick. This can be extended to model
several classes of events such as determining whether an image contains
a cat, dog, lion, etc. Each object being detected in the image would be
assigned a probability between 0 and 1, with a sum of one.

The equation for Logistic Regression can be written as:

$$
output = log{_e}(\frac{p}{1-p}) = \beta_0 + \beta_1 x + \beta_2 x^2 + ... + \beta_n x^n \
$$ The “output” is also called logit. Another name for “output” is the
log odds ratio. p is the probability of an event occuring or not. So the
odds ratio is: (Probability of an event occurring divided by probability
of an event not occurring)

$$
\frac{p}{1-p}
$$ Suppose: $$
\begin{aligned}
        Y = \beta_0 + \beta_1 x + \beta_2 x^2 + ... + \beta_n x^n  \\   
\end{aligned}
$$

Then

$$
log{_e}(\frac{p}{1-p}) = Y \\
$$ Taking log on both the sides

$$
\\
\frac{p}{1-p} = e^Y \\
$$

Solving for p, we will get

$$
p = \frac{e^Y}{1+e^Y} \\
$$ As Y increases positively p approaches 1 and as Y increases
negatively, then p approaches to zero

``` r
library(readr)
# Use read_csv() to read the file 
file_location <- paste0(getwd(), "/../Input/UCLA_Student_Admissions.csv")
admissions <- read_csv(file_location)
```

    ## Rows: 400 Columns: 4
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl (4): admit, gre, gpa, rank
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
#df <- read_csv(file.choose())
```

``` r
admissions$rank <- factor(admissions$rank)
```

``` r
library(tibble) 
glimpse(admissions)
```

    ## Rows: 400
    ## Columns: 4
    ## $ admit <dbl> 0, 1, 1, 1, 0, 1, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 1…
    ## $ gre   <dbl> 380, 660, 800, 640, 520, 760, 560, 400, 540, 700, 800, 440, 760,…
    ## $ gpa   <dbl> 3.61, 3.67, 4.00, 3.19, 2.93, 3.00, 2.98, 3.08, 3.39, 3.92, 4.00…
    ## $ rank  <fct> 3, 3, 1, 4, 4, 2, 1, 2, 3, 2, 4, 1, 1, 2, 1, 3, 4, 3, 2, 1, 3, 2…

``` r
# Include your code to select train and test samples 
# use the seed 100 for selecting the random samples for reproducibility 
# Use 80% of your data to create a training sample 
# Use 20% of your data to create a test sample 
admissions$sample_col <- sample(c(1,2), nrow(admissions), 
                     replace = T, prob = c(0.8, 0.2))
train <- admissions[admissions$sample_col ==1, ]
test <- admissions[admissions$sample_col == 2, ]
```

``` r
# Include your code to run the Generalized Linear Regression (GLM) model of "binomial" family
# Print the summary of the model 
# The model returns coefficients that impact the outcome variable admit 
# Interpret the results in terms of log odds 
model <- glm(admit ~ gre+gpa+rank,
             family = "binomial",
             data = train)
summary(model)
```

    ## 
    ## Call:
    ## glm(formula = admit ~ gre + gpa + rank, family = "binomial", 
    ##     data = train)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.5653  -0.8875  -0.6030   1.1140   2.1786  
    ## 
    ## Coefficients:
    ##              Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept) -3.516813   1.333884  -2.637 0.008376 ** 
    ## gre          0.001703   0.001258   1.354 0.175843    
    ## gpa          0.763732   0.388283   1.967 0.049190 *  
    ## rank2       -0.593510   0.353286  -1.680 0.092964 .  
    ## rank3       -1.422077   0.395915  -3.592 0.000328 ***
    ## rank4       -1.906431   0.505267  -3.773 0.000161 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 383.01  on 306  degrees of freedom
    ## Residual deviance: 347.56  on 301  degrees of freedom
    ## AIC: 359.56
    ## 
    ## Number of Fisher Scoring iterations: 4

``` r
# Make predictions for the train sample
# Create a confusion matrix using the train sample and calculate the accuracy of the model using training sample  
predicted_admit <- predict(model,
                           train[-5], type = "response") #ignoring the fifth column 
head(predicted_admit)
```

    ##          1          2          3          4          5          6 
    ## 0.17728355 0.26652380 0.71097624 0.13041129 0.09110641 0.37163431

``` r
predicted_admit <- ifelse(predicted_admit > 0.5, 1, 0)
```

``` r
train$prediction <- predicted_admit
confusionMatrix <- table(train$admit, train$prediction)
confusionMatrix <- as.data.frame(confusionMatrix)
#View(confusionMatrix)
accuracy <- sum(confusionMatrix[
  confusionMatrix$Var1 == confusionMatrix$Var2, "Freq"])/
  sum(confusionMatrix$Fre)
print(accuracy)
```

    ## [1] 0.713355

``` r
# Make predictions for the test sample
# Create a confusion matrix using the train sample and calculate the accuracy of the model using training sample  
predicted_admit1 <- predict(model,
                           test[-5], type = "response") #ignoring the fifth column 
head(predicted_admit1)
```

    ##          1          2          3          4          5          6 
    ## 0.51880862 0.42348386 0.67477852 0.08542428 0.52888970 0.43587856

``` r
predicted_admit1 <- ifelse(predicted_admit1 > 0.5, 1, 0)
```

``` r
test$prediction <- predicted_admit1
confusionMatrix1 <- table(test$admit, test$prediction)
confusionMatrix1 <- as.data.frame(confusionMatrix1)
#View(confusionMatrix)
accuracy <- sum(confusionMatrix1[
  confusionMatrix1$Var1 == confusionMatrix1$Var2, "Freq"])/
  sum(confusionMatrix1$Fre)
print(accuracy)
```

    ## [1] 0.6989247

``` r
exp(model$coefficients)
```

    ## (Intercept)         gre         gpa       rank2       rank3       rank4 
    ##  0.02969392  1.00170397  2.14627064  0.55238525  0.24121240  0.14860978
