# Class 09: Halloween Mini-Project
Josie (A11433761)

## 1: Import data

``` r
candy_file<-"candy-data.csv"
candy<-read.csv(candy_file, row.names = 1)
head(candy)
```

                 chocolate fruity caramel peanutyalmondy nougat crispedricewafer
    100 Grand            1      0       1              0      0                1
    3 Musketeers         1      0       0              0      1                0
    One dime             0      0       0              0      0                0
    One quarter          0      0       0              0      0                0
    Air Heads            0      1       0              0      0                0
    Almond Joy           1      0       0              1      0                0
                 hard bar pluribus sugarpercent pricepercent winpercent
    100 Grand       0   1        0        0.732        0.860   66.97173
    3 Musketeers    0   1        0        0.604        0.511   67.60294
    One dime        0   0        0        0.011        0.116   32.26109
    One quarter     0   0        0        0.011        0.511   46.11650
    Air Heads       0   0        0        0.906        0.511   52.34146
    Almond Joy      0   1        0        0.465        0.767   50.34755

``` r
nrow(candy)
```

    [1] 85

``` r
sum(candy$fruity)
```

    [1] 38

``` r
dim(candy)
```

    [1] 85 12

## 2: Favorite Candy

``` r
candy["Dum Dums",]$winpercent
```

    [1] 39.46056

``` r
library(dplyr)
```


    Attaching package: 'dplyr'

    The following objects are masked from 'package:stats':

        filter, lag

    The following objects are masked from 'package:base':

        intersect, setdiff, setequal, union

``` r
candy|>
filter( rownames(candy)=="Dum Dums")|>
  select(winpercent)
```

             winpercent
    Dum Dums   39.46056

``` r
candy|>
filter( rownames(candy)=="Kit Kat")|>
  select(winpercent)
```

            winpercent
    Kit Kat    76.7686

``` r
candy|>
  filter(rownames(candy)%in% c("Kit Kat", "Tootsie Roll Snack Bars"))|>
  select(winpercent)
```

                            winpercent
    Kit Kat                    76.7686
    Tootsie Roll Snack Bars    49.6535

`%in%` operator useful for checking the intersection

Install “skimr” in console

``` r
library("skimr")
skim(candy)
```

|                                                  |       |
|:-------------------------------------------------|:------|
| Name                                             | candy |
| Number of rows                                   | 85    |
| Number of columns                                | 12    |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |       |
| Column type frequency:                           |       |
| numeric                                          | 12    |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |       |
| Group variables                                  | None  |

Data summary

**Variable type: numeric**

| skim_variable | n_missing | complete_rate | mean | sd | p0 | p25 | p50 | p75 | p100 | hist |
|:---|---:|---:|---:|---:|---:|---:|---:|---:|---:|:---|
| chocolate | 0 | 1 | 0.44 | 0.50 | 0.00 | 0.00 | 0.00 | 1.00 | 1.00 | ▇▁▁▁▆ |
| fruity | 0 | 1 | 0.45 | 0.50 | 0.00 | 0.00 | 0.00 | 1.00 | 1.00 | ▇▁▁▁▆ |
| caramel | 0 | 1 | 0.16 | 0.37 | 0.00 | 0.00 | 0.00 | 0.00 | 1.00 | ▇▁▁▁▂ |
| peanutyalmondy | 0 | 1 | 0.16 | 0.37 | 0.00 | 0.00 | 0.00 | 0.00 | 1.00 | ▇▁▁▁▂ |
| nougat | 0 | 1 | 0.08 | 0.28 | 0.00 | 0.00 | 0.00 | 0.00 | 1.00 | ▇▁▁▁▁ |
| crispedricewafer | 0 | 1 | 0.08 | 0.28 | 0.00 | 0.00 | 0.00 | 0.00 | 1.00 | ▇▁▁▁▁ |
| hard | 0 | 1 | 0.18 | 0.38 | 0.00 | 0.00 | 0.00 | 0.00 | 1.00 | ▇▁▁▁▂ |
| bar | 0 | 1 | 0.25 | 0.43 | 0.00 | 0.00 | 0.00 | 0.00 | 1.00 | ▇▁▁▁▂ |
| pluribus | 0 | 1 | 0.52 | 0.50 | 0.00 | 0.00 | 1.00 | 1.00 | 1.00 | ▇▁▁▁▇ |
| sugarpercent | 0 | 1 | 0.48 | 0.28 | 0.01 | 0.22 | 0.47 | 0.73 | 0.99 | ▇▇▇▇▆ |
| pricepercent | 0 | 1 | 0.47 | 0.29 | 0.01 | 0.26 | 0.47 | 0.65 | 0.98 | ▇▇▇▇▆ |
| winpercent | 0 | 1 | 50.32 | 14.71 | 22.45 | 39.14 | 47.83 | 59.86 | 84.18 | ▃▇▆▅▂ |

Q6:winpercent column is on a very different scale than the rest of the
data. It will need to be scaled.

``` r
hist(candy$winpercent)
```

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-10-1.png)

``` r
library(ggplot2)

ggplot(candy)+ aes(winpercent)+
  geom_histogram(bins=10)+
  theme_bw()
```

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-11-1.png)

``` r
summary(candy$winpercent)
```

       Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
      22.45   39.14   47.83   50.32   59.86   84.18 

Q11: Chocolate ranks higher than fruity candy

``` r
inds<-candy$chocolate==1
candy[inds,]$winpercent
```

     [1] 66.97173 67.60294 50.34755 56.91455 38.97504 55.37545 62.28448 56.49050
     [9] 59.23612 57.21925 76.76860 71.46505 66.57458 55.06407 73.09956 60.80070
    [17] 64.35334 47.82975 54.52645 70.73564 66.47068 69.48379 81.86626 84.18029
    [25] 73.43499 72.88790 65.71629 34.72200 37.88719 76.67378 59.52925 48.98265
    [33] 43.06890 45.73675 49.65350 81.64291 49.52411

``` r
chocolate.win<-candy|>
  filter(chocolate==1)|>
  select(winpercent)
```

``` r
fruit.win<-candy|>
  filter(fruity==1)|>
  select(winpercent)
```

``` r
t.test(fruit.win,chocolate.win)
```


        Welch Two Sample t-test

    data:  fruit.win and chocolate.win
    t = -6.2582, df = 68.882, p-value = 2.871e-08
    alternative hypothesis: true difference in means is not equal to 0
    95 percent confidence interval:
     -22.15795 -11.44563
    sample estimates:
    mean of x mean of y 
     44.11974  60.92153 

## 3: Candy Rankings

Lowest ranking candies: Nik L Nip,Boston Baked Beans,Chiclets,Super
Bubble,Jawbusters Highest ranking candies: Reese’s Peanut Butter
cup,Reese’s Miniatures,Twix,Kit Kat,Snickers

``` r
head(candy[order(candy$winpercent),], n=5)
```

                       chocolate fruity caramel peanutyalmondy nougat
    Nik L Nip                  0      1       0              0      0
    Boston Baked Beans         0      0       0              1      0
    Chiclets                   0      1       0              0      0
    Super Bubble               0      1       0              0      0
    Jawbusters                 0      1       0              0      0
                       crispedricewafer hard bar pluribus sugarpercent pricepercent
    Nik L Nip                         0    0   0        1        0.197        0.976
    Boston Baked Beans                0    0   0        1        0.313        0.511
    Chiclets                          0    0   0        1        0.046        0.325
    Super Bubble                      0    0   0        0        0.162        0.116
    Jawbusters                        0    1   0        1        0.093        0.511
                       winpercent
    Nik L Nip            22.44534
    Boston Baked Beans   23.41782
    Chiclets             24.52499
    Super Bubble         27.30386
    Jawbusters           28.12744

``` r
sort(candy$winpercent)
```

     [1] 22.44534 23.41782 24.52499 27.30386 28.12744 29.70369 32.23100 32.26109
     [9] 33.43755 34.15896 34.51768 34.57899 34.72200 35.29076 36.01763 37.34852
    [17] 37.72234 37.88719 38.01096 38.97504 39.01190 39.14106 39.18550 39.44680
    [25] 39.46056 41.26551 41.38956 41.90431 42.17877 42.27208 42.84914 43.06890
    [33] 43.08892 44.37552 45.46628 45.73675 45.99583 46.11650 46.29660 46.41172
    [41] 46.78335 47.17323 47.82975 48.98265 49.52411 49.65350 50.34755 51.41243
    [49] 52.34146 52.82595 52.91139 54.52645 54.86111 55.06407 55.10370 55.35405
    [57] 55.37545 56.49050 56.91455 57.11974 57.21925 59.23612 59.52925 59.86400
    [65] 60.80070 62.28448 63.08514 64.35334 65.71629 66.47068 66.57458 66.97173
    [73] 67.03763 67.60294 69.48379 70.73564 71.46505 72.88790 73.09956 73.43499
    [81] 76.67378 76.76860 81.64291 81.86626 84.18029

``` r
inds<-order(candy$winpercent)
head(candy[inds,])
```

                       chocolate fruity caramel peanutyalmondy nougat
    Nik L Nip                  0      1       0              0      0
    Boston Baked Beans         0      0       0              1      0
    Chiclets                   0      1       0              0      0
    Super Bubble               0      1       0              0      0
    Jawbusters                 0      1       0              0      0
    Root Beer Barrels          0      0       0              0      0
                       crispedricewafer hard bar pluribus sugarpercent pricepercent
    Nik L Nip                         0    0   0        1        0.197        0.976
    Boston Baked Beans                0    0   0        1        0.313        0.511
    Chiclets                          0    0   0        1        0.046        0.325
    Super Bubble                      0    0   0        0        0.162        0.116
    Jawbusters                        0    1   0        1        0.093        0.511
    Root Beer Barrels                 0    1   0        1        0.732        0.069
                       winpercent
    Nik L Nip            22.44534
    Boston Baked Beans   23.41782
    Chiclets             24.52499
    Super Bubble         27.30386
    Jawbusters           28.12744
    Root Beer Barrels    29.70369

``` r
inds<-order(candy$winpercent,decreasing=T)
head(candy[inds,],5)
```

                              chocolate fruity caramel peanutyalmondy nougat
    Reese's Peanut Butter cup         1      0       0              1      0
    Reese's Miniatures                1      0       0              1      0
    Twix                              1      0       1              0      0
    Kit Kat                           1      0       0              0      0
    Snickers                          1      0       1              1      1
                              crispedricewafer hard bar pluribus sugarpercent
    Reese's Peanut Butter cup                0    0   0        0        0.720
    Reese's Miniatures                       0    0   0        0        0.034
    Twix                                     1    0   1        0        0.546
    Kit Kat                                  1    0   1        0        0.313
    Snickers                                 0    0   1        0        0.546
                              pricepercent winpercent
    Reese's Peanut Butter cup        0.651   84.18029
    Reese's Miniatures               0.279   81.86626
    Twix                             0.906   81.64291
    Kit Kat                          0.511   76.76860
    Snickers                         0.651   76.67378

``` r
ggplot(candy)+
  aes(x=winpercent, y=reorder(rownames(candy),winpercent))+
  geom_col()
```

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-19-1.png)

``` r
my_cols=rep("black", nrow(candy))
my_cols[as.logical(candy$chocolate)] = "chocolate"
my_cols[as.logical(candy$bar)] = "brown"
my_cols[as.logical(candy$fruity)] = "pink"
ggplot(candy)+
  aes(x=winpercent, y=reorder(rownames(candy),winpercent))+
  geom_col(fill=my_cols)
```

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-20-1.png)

Worst chocolate ranked: Sixlets Best fruity candy ranked: Starbursts

``` r
#Finding Sour Patch Kids and coloring the bar

my_cols=rep("black", nrow(candy))
my_cols[as.logical(candy$chocolate)] = "chocolate"
my_cols[as.logical(candy$bar)] = "brown"
my_cols[as.logical(candy$fruity)] = "pink"
my_cols[rownames(candy)=="Sour Patch Kids"] = "blue"
ggplot(candy)+
  aes(x=winpercent, y=reorder(rownames(candy),winpercent))+
  geom_col(fill=my_cols)
```

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-21-1.png)

``` r
ord <- order(candy$pricepercent, decreasing = TRUE)
head( candy[ord,c(11,12)], n=5 )
```

                             pricepercent winpercent
    Nik L Nip                       0.976   22.44534
    Nestle Smarties                 0.976   37.88719
    Ring pop                        0.965   35.29076
    Hershey's Krackel               0.918   62.28448
    Hershey's Milk Chocolate        0.918   56.49050

## 4:Taking a look at pricepercent

``` r
library(ggrepel)

ggplot(candy) +
  aes(winpercent, pricepercent, label=rownames(candy)) +
  geom_point(col=my_cols) + 
  geom_text_repel(col=my_cols, size=3.3, max.overlaps = 8)
```

    Warning: ggrepel: 21 unlabeled data points (too many overlaps). Consider
    increasing max.overlaps

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-23-1.png)

## 5: Exploring the correlation structure

``` r
library(corrplot)
```

    corrplot 0.95 loaded

``` r
cij <- cor(candy)
corrplot(cij)
```

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-24-1.png)

## 6: Principal Component Analysis

``` r
pca <- prcomp(candy,scale=TRUE )
summary(pca)
```

    Importance of components:
                              PC1    PC2    PC3     PC4    PC5     PC6     PC7
    Standard deviation     2.0788 1.1378 1.1092 1.07533 0.9518 0.81923 0.81530
    Proportion of Variance 0.3601 0.1079 0.1025 0.09636 0.0755 0.05593 0.05539
    Cumulative Proportion  0.3601 0.4680 0.5705 0.66688 0.7424 0.79830 0.85369
                               PC8     PC9    PC10    PC11    PC12
    Standard deviation     0.74530 0.67824 0.62349 0.43974 0.39760
    Proportion of Variance 0.04629 0.03833 0.03239 0.01611 0.01317
    Cumulative Proportion  0.89998 0.93832 0.97071 0.98683 1.00000

``` r
plot(pca$x[,2],col=my_cols,pch=16)
```

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-26-1.png)

ggplot version

``` r
my_data <- cbind(candy, pca$x[,1:3])
p<-ggplot(my_data)+
  aes(x=PC1, y=PC2,
        size=winpercent/100,  
            text=rownames(my_data),
            label=rownames(my_data)) +
        geom_point(col=my_cols)
p
```

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-27-1.png)

``` r
p + geom_text_repel(size=3.3, col=my_cols, max.overlaps = 20)  + 
  theme(legend.position = "none") +
  labs(title="Halloween Candy PCA Space",
       subtitle="Colored by type: chocolate bar (dark brown), chocolate other (light brown), fruity (red), other (black)",
       caption="Data from 538")
```

    Warning: ggrepel: 4 unlabeled data points (too many overlaps). Consider
    increasing max.overlaps

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-28-1.png)

``` r
par(mar=c(8,4,2,2))
barplot(pca$rotation[,1], las=2, ylab="PC1 Contribution")
```

![](class09candyminiproject_files/figure-commonmark/unnamed-chunk-29-1.png)

Q24: Fruity,hard and pluribus make sense to be correlated with each
other because that is how that type of candy is usually seen. The PC1
reflects that.
