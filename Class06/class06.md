# Class06
Josie A11433761

My first function

``` r
add<-function(x,y=1){
  x+y
}
```

``` r
add(1,1)
```

    [1] 2

``` r
add(x=1, y=100)
```

    [1] 101

``` r
add(c(100, 1, 100),1)
```

    [1] 101   2 101

``` r
add(10)
```

    [1] 11

``` r
add(10,10)
```

    [1] 20

``` r
generate_DNA<-function(length){
bases<-c("A","C","T","G")
sequence<-sample(bases, size=length, 
                 replace=TRUE)
  return(sequence)
}

generate_DNA(10)  
```

     [1] "A" "T" "G" "C" "C" "G" "C" "A" "G" "T"

``` r
unique(bio3d::aa.table$aa1)[1:20]
```

     [1] "A" "R" "N" "D" "C" "Q" "E" "G" "H" "I" "L" "K" "M" "F" "P" "S" "T" "W" "Y"
    [20] "V"

``` r
generate_protein<-function(length){
bases<-c(unique(bio3d::aa.table$aa1)[1:20])
sequence<-sample(bases, size=length, 
                 replace=TRUE)
 sequence<-paste(sequence, collapse="")
 return(sequence)
}

generate_protein(10)  
```

    [1] "EDQAGSPLIQ"

``` r
#sequence was override by paste, collapse="" eliminated quotations between AAs
```

Generate sequences of length 6 to 12

``` r
answer<-sapply(6:12, generate_protein)
answer
```

    [1] "WGVTQS"       "MQAEGID"      "VNFCYCDL"     "TRPRTWYAY"    "VRQSKCEFNG"  
    [6] "DKECPEWYCKE"  "FNVAQPTLEEQH"

``` r
cat(paste(">id.",6:12,"\n",answer,sep=""),sep="\n")
```

    >id.6
    WGVTQS
    >id.7
    MQAEGID
    >id.8
    VNFCYCDL
    >id.9
    TRPRTWYAY
    >id.10
    VRQSKCEFNG
    >id.11
    DKECPEWYCKE
    >id.12
    FNVAQPTLEEQH
