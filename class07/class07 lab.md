# Class 07
Josie (A11433761)

Before we get into clustering methods let’s make some sample data to
cluster where we know what the answer should be.

To help with this I will use the `rnorm()` function.

``` r
hist(rnorm(150000,mean=-3))
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-1-1.png)

``` r
n=10000
hist(c(rnorm(n,mean=3),rnorm (n,mean=-3)))
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-2-1.png)

``` r
n=30
x<-c(rnorm(n,mean=3),rnorm (n,mean=-3))
y<-rev(x)
z<-cbind(x,y)
z
```

                  x         y
     [1,]  2.971195 -2.596147
     [2,]  1.075875 -3.472302
     [3,]  3.629690 -2.896939
     [4,]  2.847106 -3.741141
     [5,]  2.721236 -4.358647
     [6,]  2.756895 -2.693342
     [7,]  3.070808 -4.219894
     [8,]  1.727595 -3.972647
     [9,]  1.993075 -1.876100
    [10,]  3.033174 -3.317049
    [11,]  4.414430 -2.917498
    [12,]  3.728146 -4.420728
    [13,]  1.232154 -3.011692
    [14,]  3.359775 -1.628446
    [15,]  3.374427 -2.443345
    [16,]  3.669064 -2.766030
    [17,]  2.541332 -2.603731
    [18,]  2.537535 -3.338787
    [19,]  3.040898 -4.106105
    [20,]  3.263635 -2.623911
    [21,]  5.023316 -2.818835
    [22,]  1.530741 -1.680685
    [23,]  4.374135 -1.733724
    [24,]  1.430312 -4.009042
    [25,]  2.905310 -2.465969
    [26,]  4.003705 -1.371424
    [27,]  4.028462 -2.348172
    [28,]  2.106006 -1.860438
    [29,]  2.499732 -1.980122
    [30,]  1.636759 -3.318679
    [31,] -3.318679  1.636759
    [32,] -1.980122  2.499732
    [33,] -1.860438  2.106006
    [34,] -2.348172  4.028462
    [35,] -1.371424  4.003705
    [36,] -2.465969  2.905310
    [37,] -4.009042  1.430312
    [38,] -1.733724  4.374135
    [39,] -1.680685  1.530741
    [40,] -2.818835  5.023316
    [41,] -2.623911  3.263635
    [42,] -4.106105  3.040898
    [43,] -3.338787  2.537535
    [44,] -2.603731  2.541332
    [45,] -2.766030  3.669064
    [46,] -2.443345  3.374427
    [47,] -1.628446  3.359775
    [48,] -3.011692  1.232154
    [49,] -4.420728  3.728146
    [50,] -2.917498  4.414430
    [51,] -3.317049  3.033174
    [52,] -1.876100  1.993075
    [53,] -3.972647  1.727595
    [54,] -4.219894  3.070808
    [55,] -2.693342  2.756895
    [56,] -4.358647  2.721236
    [57,] -3.741141  2.847106
    [58,] -2.896939  3.629690
    [59,] -3.472302  1.075875
    [60,] -2.596147  2.971195

``` r
plot(z)
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-4-1.png)

## K-means clustering

The function in base R for k-means clustering is called `kmeans()`.

``` r
km<-kmeans(z,center=2)
km
```

    K-means clustering with 2 clusters of sizes 30, 30

    Cluster means:
              x         y
    1 -2.886386  2.884217
    2  2.884217 -2.886386

    Clustering vector:
     [1] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1
    [39] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

    Within cluster sum of squares by cluster:
    [1] 51.35439 51.35439
     (between_SS / total_SS =  90.7 %)

    Available components:

    [1] "cluster"      "centers"      "totss"        "withinss"     "tot.withinss"
    [6] "betweenss"    "size"         "iter"         "ifault"      

``` r
km$centers
```

              x         y
    1 -2.886386  2.884217
    2  2.884217 -2.886386

``` r
km$cluster
```

     [1] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1
    [39] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

``` r
plot(z,col=c("red","blue"))
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-8-1.png)

``` r
plot(z, col=c(1,2))
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-9-1.png)

``` r
plot(z, col=km$cluster) #plot with clustering results and cluster centers
points(km$centers, col="blue",pch=15,cex=2) #color the center and make it a square center (pch=15)
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-10-1.png)

Can you cluster our data in `z` into four clusters?

``` r
km4<-kmeans(z,center=4)
plot(z,col=km4$cluster)
points(km4$centers, col="blue",pch=15,cex=2)
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-11-1.png)

## Hierarchical Clustering

The main function for hierarchical clustering is base R is called
`hclust()`. Unlike `kmeans()` I cannot just pass in my data as input. I
first need a distance matrix from my data.

``` r
d<-dist(z)
hc<-hclust(d)
hc
```


    Call:
    hclust(d = d)

    Cluster method   : complete 
    Distance         : euclidean 
    Number of objects: 60 

hclust plot method

``` r
plot(hc)
abline(h=10, col="red")
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-13-1.png)

To get my clustering results, I can “cut” my tree at a given height. To
do this, I will use the `cutree`.

``` r
grps<-cutree(hc, h=10)
```

``` r
plot(z,hc$grps)
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-15-1.png)

## Principle Component Analysis

## PCA of UK food data

``` r
url<-"http://tinyurl.com/UK-foods"
x<-read.csv(url,row.names=1)
head(x)
```

                   England Wales Scotland N.Ireland
    Cheese             105   103      103        66
    Carcass_meat       245   227      242       267
    Other_meat         685   803      750       586
    Fish               147   160      122        93
    Fats_and_oils      193   235      184       209
    Sugars             156   175      147       139

``` r
barplot(as.matrix(x), beside=T, col=rainbow(nrow(x)))
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-17-1.png)

``` r
barplot(as.matrix(x), beside=F, col=rainbow(nrow(x)))
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-18-1.png)

``` r
pairs(x, col=rainbow(10), pch=16)
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-19-1.png)

## PCA to the rescue

The main function to do PCA in base R is called `prcomp()`

``` r
pca<-prcomp(t(x))
summary(pca)
```

    Importance of components:
                                PC1      PC2      PC3       PC4
    Standard deviation     324.1502 212.7478 73.87622 2.921e-14
    Proportion of Variance   0.6744   0.2905  0.03503 0.000e+00
    Cumulative Proportion    0.6744   0.9650  1.00000 1.000e+00

Let’s see what’s inside our result object `pca`

``` r
attributes(pca)
```

    $names
    [1] "sdev"     "rotation" "center"   "scale"    "x"       

    $class
    [1] "prcomp"

``` r
pca$x
```

                     PC1         PC2        PC3           PC4
    England   -144.99315   -2.532999 105.768945 -9.152022e-15
    Wales     -240.52915 -224.646925 -56.475555  5.560040e-13
    Scotland   -91.86934  286.081786 -44.415495 -6.638419e-13
    N.Ireland  477.39164  -58.901862  -4.877895  1.329771e-13

To make our main result figure, called a PC plot (or score plot,
ordination plot, PC1 vs.PC2):

``` r
plot(pca$x[,1],pca$x[,2], col=c("black", "red","blue", "darkgreen"), pch=16, xlab="PC1 (67.4%)", ylab="PC2 (29%)")
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-23-1.png)

## Variable Loadings Plot: Lets focus on PC1 as it accounts for \> 90% of variance

``` r
par(mar=c(10, 3, 0.35, 0))
barplot( pca$rotation[,1], las=2 )
```

![](class07-lab_files/figure-commonmark/unnamed-chunk-24-1.png)

``` r
pca$rotation
```

                                 PC1          PC2         PC3          PC4
    Cheese              -0.056955380  0.016012850  0.02394295 -0.409382587
    Carcass_meat         0.047927628  0.013915823  0.06367111  0.729481922
    Other_meat          -0.258916658 -0.015331138 -0.55384854  0.331001134
    Fish                -0.084414983 -0.050754947  0.03906481  0.022375878
    Fats_and_oils       -0.005193623 -0.095388656 -0.12522257  0.034512161
    Sugars              -0.037620983 -0.043021699 -0.03605745  0.024943337
    Fresh_potatoes       0.401402060 -0.715017078 -0.20668248  0.021396007
    Fresh_Veg           -0.151849942 -0.144900268  0.21382237  0.001606882
    Other_Veg           -0.243593729 -0.225450923 -0.05332841  0.031153231
    Processed_potatoes  -0.026886233  0.042850761 -0.07364902 -0.017379680
    Processed_Veg       -0.036488269 -0.045451802  0.05289191  0.021250980
    Fresh_fruit         -0.632640898 -0.177740743  0.40012865  0.227657348
    Cereals             -0.047702858 -0.212599678 -0.35884921  0.100043319
    Beverages           -0.026187756 -0.030560542 -0.04135860 -0.018382072
    Soft_drinks          0.232244140  0.555124311 -0.16942648  0.222319484
    Alcoholic_drinks    -0.463968168  0.113536523 -0.49858320 -0.273126013
    Confectionery       -0.029650201  0.005949921 -0.05232164  0.001890737
