---
title: "Homework 5"
author: "Jim Holdnack"
date: "February 10, 2019"
output:
  html_document:
    keep_md: yes
---
###### Open and clean file y2016
1. import file -- I set the working directory to file repository and used read.table. I cleaned up the import so variables were named and had correct format
2. Display the summary and structure of df-- i used summary str
3. find mispelled name---I used grep to identify the row and then printed the row for column name.
d. Upon finding the misspelled name, please remove this particular observation I used file = and subtract specific row with erroneous name


```r
knitr::opts_chunk$set(echo = TRUE)
getwd()
```

```
## [1] "C:/Users/jhold/Desktop/rProjectEx/Homework 5"
```

```r
setwd("/Users/jhold/Desktop/homework5")
library(tidyverse)
```

```
## -- Attaching packages ---------------------------------------------------------------------------------------------------------------------------- tidyverse 1.2.1 --
```

```
## v ggplot2 3.1.0     v purrr   0.2.5
## v tibble  1.4.2     v dplyr   0.7.6
## v tidyr   0.8.1     v stringr 1.3.1
## v readr   1.1.1     v forcats 0.3.0
```

```
## -- Conflicts ------------------------------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(readr)
df <- read.table("/Users/jhold/Desktop/homework5/yob2016.txt", sep = ';' )
df$name <- as.character(df$V1)
df$sex  <- df$V2
df$Frequency <- df$V3
df <- df[-c(1,2,3)]
str(df)
```

```
## 'data.frame':	32869 obs. of  3 variables:
##  $ name     : chr  "Emma" "Olivia" "Ava" "Sophia" ...
##  $ sex      : Factor w/ 2 levels "F","M": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Frequency: int  19414 19246 16237 16070 14722 14366 13030 11699 10926 10733 ...
```

```r
summary(df)
```

```
##      name           sex         Frequency      
##  Length:32869       F:18758   Min.   :    5.0  
##  Class :character   M:14111   1st Qu.:    7.0  
##  Mode  :character             Median :   12.0  
##                               Mean   :  110.7  
##                               3rd Qu.:   30.0  
##                               Max.   :19414.0
```

```r
grep('yyy',df$name)
```

```
## [1] 212
```

```r
df$name[212]
```

```
## [1] "Fionayyy"
```

```r
y2016 <-df[-212,]
str(y2016)
```

```
## 'data.frame':	32868 obs. of  3 variables:
##  $ name     : chr  "Emma" "Olivia" "Ava" "Sophia" ...
##  $ sex      : Factor w/ 2 levels "F","M": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Frequency: int  19414 19246 16237 16070 14722 14366 13030 11699 10926 10733 ...
```

## Data Merging 
1. imported the y2015 file using read.table and did clean-up like part 1 though I had to separate by comma rather than semi-colon
2. Display the last ten rows in the dataframe I used tail command for 10 rows. All the names are boys names and all have exactly 5 as frequency of use, and all are "z" names
c. Merge y2016 and y2015 by your Name column. I merged on both name and sex to make for a cleaner merge. I used the na omit function to get rid og missing data rows - I used head 100 to make sure no missing data was present


```r
knitr::opts_chunk$set(echo = TRUE)
df2 <- read.table("/Users/jhold/Desktop/homework5/yob2015.txt", sep = ',')
df2$name <- as.character(df2$V1)
df2$sex  <- df2$V2
df2$Frequency <- df2$V3
y2015 <- df2[-c(1,2,3)]
tail(y2015,10)
```

```
##         name sex Frequency
## 33054   Ziyu   M         5
## 33055   Zoel   M         5
## 33056  Zohar   M         5
## 33057 Zolton   M         5
## 33058   Zyah   M         5
## 33059 Zykell   M         5
## 33060 Zyking   M         5
## 33061  Zykir   M         5
## 33062  Zyrus   M         5
## 33063   Zyus   M         5
```

```r
nd1 <- merge(y2016, y2015, union("name", "sex"), all=TRUE)
head(nd1,100)
```

```
##             name sex Frequency.x Frequency.y
## 1          Aaban   M           9          15
## 2          Aabha   F           7           7
## 3          Aabid   M           5          NA
## 4          Aabir   M           5          NA
## 5      Aabriella   F          11           5
## 6           Aada   F          NA           5
## 7          Aadam   M          18          22
## 8          Aadan   M          NA          10
## 9        Aadarsh   M          11          15
## 10         Aaden   M         194         297
## 11        Aadhav   M          28          31
## 12      Aadhavan   M           6           5
## 13         Aadhi   M           5          11
## 14       Aadhira   F          14           8
## 15       Aadhvik   M          19           9
## 16      Aadhvika   F           9          NA
## 17        Aadhya   F         284         265
## 18       Aadhyan   M          NA           7
## 19          Aadi   M          55          43
## 20         Aadil   M          15          14
## 21         Aadin   M          NA           5
## 22        Aadish   M           5          NA
## 23         Aadit   M          23          23
## 24        Aadith   M          11          11
## 25      Aadithya   M           5           6
## 26       Aaditri   F          11          NA
## 27       Aaditya   M          34          33
## 28         Aadiv   M          NA           6
## 29         Aadon   M           9           8
## 30       Aadrian   M          NA           7
## 31       Aadrika   F          NA           9
## 32        Aadrit   M           5          NA
## 33       Aadriti   F           5          NA
## 34         Aadvi   F           7          NA
## 35        Aadvik   M          83          28
## 36       Aadvika   F          13           7
## 37         Aadya   F         159         159
## 38         Aadyn   M          51          29
## 39         Aafia   F          NA           6
## 40        Aafiya   F           6          NA
## 41       Aafiyah   F           5          NA
## 42         Aagam   M           7           5
## 43         Aagna   F           7          NA
## 44        Aahaan   M           5          10
## 45         Aahan   M          36          26
## 46        Aahana   F          51          31
## 47         Aahil   M          81          78
## 48         Aahir   M          NA           6
## 49         Aahna   F          NA          12
## 50        Aaiden   M          71          89
## 51        Aaidyn   M           5          11
## 52         Aaila   F          11           7
## 53      Aailiyah   F          NA           5
## 54       Aailyah   F           6           6
## 55         Aaima   F          21          12
## 56         Aaira   F          31          24
## 57        Aairah   F          28          19
## 58        Aaisha   F           7          11
## 59     Aakanksha   F           5          NA
## 60        Aakash   M          21          17
## 61       Aakriti   F           5           8
## 62          Aala   F           9           6
## 63      Aalaiyah   F          10          11
## 64        Aalani   F          16          17
## 65        Aalaya   F           7           9
## 66       Aalayah   F          66          70
## 67      Aalayiah   F           5           8
## 68       Aalayna   F          NA           5
## 69      Aalaysia   F           9           9
## 70        Aaleah   F          16          11
## 71      Aaleahya   F          NA           5
## 72      Aaleayah   F           5          NA
## 73       Aaleena   F          NA           5
## 74      Aaleeyah   F           9          11
## 75       Aaleiah   F          NA           6
## 76      Aaleigha   F           7           9
## 77      Aaleiyah   F           5          NA
## 78        Aalena   F          NA           5
## 79       Aaleyah   F         104         153
## 80          Aali   M          NA           6
## 81         Aalia   F          46          33
## 82        Aaliah   F          32          46
## 83       Aaliana   F           5           6
## 84       Aalijah   F           8          12
## 85       Aalijah   M          11          17
## 86        Aalina   F           6           9
## 87       Aalinah   F          NA           6
## 88        Aalisa   F          NA           5
## 89       Aalisha   F          NA           5
## 90       Aalivia   F          NA           7
## 91        Aaliya   F          57          64
## 92       Aaliyah   F        4611        4850
## 93       Aaliyah   M          NA           5
## 94  Aaliyahmarie   F          NA           6
## 95   Aaliyahrose   F           5           5
## 96       Aaliyan   F           6          NA
## 97       Aaliyan   M           5          NA
## 98      Aaliyana   F           8           6
## 99     Aaliyanna   F          NA           5
## 100      Aaliyha   F          NA           6
```

```r
nd1$missx <-is.na(nd1$Frequency.x)
final <- na.omit(nd1)
str(final)
```

```
## 'data.frame':	26550 obs. of  5 variables:
##  $ name       : chr  "Aaban" "Aabha" "Aabriella" "Aadam" ...
##  $ sex        : Factor w/ 2 levels "F","M": 2 1 1 2 2 2 2 2 2 1 ...
##  $ Frequency.x: int  9 7 11 18 11 194 28 6 5 14 ...
##  $ Frequency.y: int  15 7 5 22 15 297 31 5 11 8 ...
##  $ missx      : logi  FALSE FALSE FALSE FALSE FALSE FALSE ...
##  - attr(*, "na.action")= 'omit' Named int  3 4 6 8 16 18 21 22 26 28 ...
##   ..- attr(*, "names")= chr  "3" "4" "6" "8" ...
```

```r
final <- final[c(1,2,3,4)]
head(final,100)
```

```
##            name sex Frequency.x Frequency.y
## 1         Aaban   M           9          15
## 2         Aabha   F           7           7
## 5     Aabriella   F          11           5
## 7         Aadam   M          18          22
## 9       Aadarsh   M          11          15
## 10        Aaden   M         194         297
## 11       Aadhav   M          28          31
## 12     Aadhavan   M           6           5
## 13        Aadhi   M           5          11
## 14      Aadhira   F          14           8
## 15      Aadhvik   M          19           9
## 17       Aadhya   F         284         265
## 19         Aadi   M          55          43
## 20        Aadil   M          15          14
## 23        Aadit   M          23          23
## 24       Aadith   M          11          11
## 25     Aadithya   M           5           6
## 27      Aaditya   M          34          33
## 29        Aadon   M           9           8
## 35       Aadvik   M          83          28
## 36      Aadvika   F          13           7
## 37        Aadya   F         159         159
## 38        Aadyn   M          51          29
## 42        Aagam   M           7           5
## 44       Aahaan   M           5          10
## 45        Aahan   M          36          26
## 46       Aahana   F          51          31
## 47        Aahil   M          81          78
## 50       Aaiden   M          71          89
## 51       Aaidyn   M           5          11
## 52        Aaila   F          11           7
## 54      Aailyah   F           6           6
## 55        Aaima   F          21          12
## 56        Aaira   F          31          24
## 57       Aairah   F          28          19
## 58       Aaisha   F           7          11
## 60       Aakash   M          21          17
## 61      Aakriti   F           5           8
## 62         Aala   F           9           6
## 63     Aalaiyah   F          10          11
## 64       Aalani   F          16          17
## 65       Aalaya   F           7           9
## 66      Aalayah   F          66          70
## 67     Aalayiah   F           5           8
## 69     Aalaysia   F           9           9
## 70       Aaleah   F          16          11
## 74     Aaleeyah   F           9          11
## 76     Aaleigha   F           7           9
## 79      Aaleyah   F         104         153
## 81        Aalia   F          46          33
## 82       Aaliah   F          32          46
## 83      Aaliana   F           5           6
## 84      Aalijah   F           8          12
## 85      Aalijah   M          11          17
## 86       Aalina   F           6           9
## 91       Aaliya   F          57          64
## 92      Aaliyah   F        4611        4850
## 95  Aaliyahrose   F           5           5
## 98     Aaliyana   F           8           6
## 101    Aaliyiah   F           5           5
## 104      Aalyah   F          14          23
## 105     Aalyiah   F          23          23
## 108     Aamanee   F           5           5
## 109      Aamani   F          23           7
## 110      Aamari   F           5           9
## 111      Aamari   M          14           7
## 115     Aamilah   F          15          12
## 116      Aamina   F          24          24
## 117     Aaminah   F          27          42
## 118       Aamir   M         132         143
## 119      Aamira   F          25          37
## 120     Aamirah   F          10          15
## 121      Aamiya   F           8           5
## 122     Aamiyah   F          30          25
## 123       Aamna   F          11           6
## 125      Aamori   F           6           7
## 129      Aanaya   F          14           8
## 130       Aania   F           6           5
## 131      Aanika   F          20          24
## 132      Aaniya   F          27          17
## 133     Aaniyah   F          48          54
## 135      Aanshi   F          13          12
## 136       Aanvi   F          41          47
## 137       Aanya   F         214         240
## 138       Aaqil   M           7           7
## 139        Aara   F          13          15
## 142   Aaradhana   F          13           8
## 144    Aaradhya   F         102          81
## 146     Aaralyn   F          73          72
## 147    Aaralynn   F          13          22
## 148       Aaran   M           9          17
## 149       Aarav   M         519         539
## 150      Aaravi   F           5           7
## 153       Aaren   M          31          22
## 156       Aaria   F          62          36
## 157      Aariah   F          32          26
## 158      Aarian   F           5           8
## 159      Aarian   M          17          13
## 160     Aariana   F          16          27
## 161    Aarianna   F          18          10
```

## Data Summary 
1. create a new column of total frequency -- I added frequency.x + frequency.y
2. I sorted by total and found the top names were Emma Olivia Noah Liam Sophia Ava Mason William Jacob Isabella
3.  I dropped all the boys and created a new date frame if just girls names by using sex =F, I sorted by total and listed the top girl names
Emma Olivia Sophia Ava Isabella Mia Charlotte Abigail Emily Harper 
4. I wrote the results of the topten girls names to a file called TopGirlNames by selecting only frequencies > 21000

All output should be in github https://github.com/holdwork/Homework.git



```r
knitr::opts_chunk$set(echo = TRUE)
final$total <- final$Frequency.x + final$Frequency.y
summary(final)
```

```
##      name           sex        Frequency.x       Frequency.y     
##  Length:26550       F:15267   Min.   :    5.0   Min.   :    5.0  
##  Class :character   M:11283   1st Qu.:    8.0   1st Qu.:    8.0  
##  Mode  :character             Median :   15.0   Median :   16.0  
##                               Mean   :  135.5   Mean   :  137.2  
##                               3rd Qu.:   41.0   3rd Qu.:   41.0  
##                               Max.   :19414.0   Max.   :20415.0  
##      total        
##  Min.   :   10.0  
##  1st Qu.:   17.0  
##  Median :   31.0  
##  Mean   :  272.7  
##  3rd Qu.:   81.0  
##  Max.   :39829.0
```

```r
finalSort <- final[order(-final$total),]
head(finalSort,10)
```

```
##           name sex Frequency.x Frequency.y total
## 12027     Emma   F       19414       20415 39829
## 29240   Olivia   F       19246       19638 38884
## 28798     Noah   M       19015       19594 38609
## 23620     Liam   M       18138       18330 36468
## 34320   Sophia   F       16070       17381 33451
## 4759       Ava   F       16237       16340 32577
## 25956    Mason   M       15192       16591 31783
## 37328  William   M       15668       15863 31531
## 15977    Jacob   M       14416       15914 30330
## 15521 Isabella   F       14722       15574 30296
```

```r
finalF <- final[final$sex=='F',c(1:5)]
finalFsort <- finalF[order(-finalF$total),]
head(finalFsort,10)
```

```
##            name sex Frequency.x Frequency.y total
## 12027      Emma   F       19414       20415 39829
## 29240    Olivia   F       19246       19638 38884
## 34320    Sophia   F       16070       17381 33451
## 4759        Ava   F       16237       16340 32577
## 15521  Isabella   F       14722       15574 30296
## 26751       Mia   F       14366       14871 29237
## 7961  Charlotte   F       13030       11381 24411
## 428     Abigail   F       11699       12371 24070
## 12001     Emily   F       10926       11766 22692
## 14502    Harper   F       10733       10283 21016
```

```r
finalExport <- finalFsort[finalFsort$total > 21000, c(1,5)]
write.csv(finalExport, file="/Users/jhold/Desktop/homework5/TopGirlNames.csv")
```


