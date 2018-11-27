Homework 6
================
Vincent Tam
November 25, 2018

Problem 1 - Homicide Data

    ## -- Attaching packages ----------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.0.0     v purrr   0.2.5
    ## v tibble  1.4.2     v dplyr   0.7.6
    ## v tidyr   0.8.1     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## -- Conflicts -------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

![](hw6_files/figure-markdown_github/all%20cities%20homicides-1.png) Problem 2 - Birthweight

    ## Loading required package: nlme

    ## 
    ## Attaching package: 'nlme'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     collapse

    ## This is mgcv 1.8-25. For overview type 'help("mgcv-package")'.

| term        |  estimate|  p.value|
|:------------|---------:|--------:|
| (Intercept) |  2722.294|        0|
| ppbmi       |   -36.777|        0|
| ppwt        |     9.599|        0|

    ##    bwt    ppbmi ppwt      resid     pred
    ## 1 3629 26.27184  148  452.23247 3176.768
    ## 2 3062 21.34485  128 -103.98493 3165.985
    ## 3 3345 23.56517  137  174.27945 3170.721
    ## 4 3062 21.84508  127  -75.98865 3137.989
    ## 5 3374 21.02642  130  177.10566 3196.894
    ## 6 3374 18.60030  115  231.86726 3142.133

![](hw6_files/figure-markdown_github/maternal%20factors%20bmi%20and%20wt-1.png)![](hw6_files/figure-markdown_github/maternal%20factors%20bmi%20and%20wt-2.png)

| term        |   estimate|  p.value|
|:------------|----------:|--------:|
| (Intercept) |  -4347.667|        0|
| blength     |    128.556|        0|
| gaweeks     |     27.047|        0|

    ##    bwt blength gaweeks     resid     pred
    ## 1 3629      51    39.9  341.1622 3287.838
    ## 2 3062      48    25.9  538.4835 2523.516
    ## 3 3345      50    39.9  185.7178 3159.282
    ## 4 3062      52    40.0 -357.0982 3419.098
    ## 5 3374      52    41.6  -88.3729 3462.373
    ## 6 3374      52    40.7  -64.0309 3438.031

| term                   |   estimate|  p.value|
|:-----------------------|----------:|--------:|
| (Intercept)            |  -7176.817|    0.000|
| bhead                  |    181.796|    0.000|
| blength                |    102.127|    0.000|
| babysex2               |   6374.868|    0.000|
| bhead:blength          |     -0.554|    0.478|
| bhead:babysex2         |   -198.393|    0.000|
| blength:babysex2       |   -123.773|    0.000|
| bhead:blength:babysex2 |      3.878|    0.000|

    ##    bwt bhead blength babysex      resid     pred
    ## 1 3629    34      51       2  334.62431 3294.376
    ## 2 3062    34      48       1   59.16394 3002.836
    ## 3 3345    36      50       2 -157.23983 3502.240
    ## 4 3062    34      52       1 -274.05285 3336.053
    ## 5 3374    34      52       2  -11.76080 3385.761
    ## 6 3374    33      52       1  190.95508 3183.045

![](hw6_files/figure-markdown_github/crossvalidation%20of%20models-1.png)
