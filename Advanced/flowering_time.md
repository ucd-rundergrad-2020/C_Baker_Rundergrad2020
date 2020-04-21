---
title: "Flowering Time"
author: "Cassandra"
date: "4/21/2020"
output: 
  html_document: 
    keep_md: yes
---


```r
library(tidyverse)
```

```
## -- Attaching packages ---------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.0     v purrr   0.3.3
## v tibble  3.0.0     v dplyr   0.8.5
## v tidyr   1.0.2     v stringr 1.4.0
## v readr   1.3.1     v forcats 0.5.0
```

```
## -- Conflicts ------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
data <- read.csv("master_flowering_time_data_2019_10_15.csv")
```

## Data discovery

**Redundant variables? Related variables? Experimental setup?**  


```r
head(data)
```

```
##   ï..DNA_ID field_ID genotype group   row   end. condition       germ
## 1      D132 SUN_A_01       WT     A SUN_A    end       sun 06_07_2019
## 2      D133 SUN_A_02       WT     A SUN_A    end       sun 06_08_2019
## 3      D134 SUN_A_03       WT     A SUN_A middle       sun 06_08_2019
## 4      D136 SUN_A_09       WT     A SUN_A middle       sun 06_08_2019
## 5      D137 SUN_A_10       WT     A SUN_A middle       sun 06_08_2019
## 6      D138 SUN_A_11       WT     A SUN_A middle       sun 06_08_2019
##       yellow  flowering      final diameter direction height leaf_num ax_heads
## 1 07_30_2019 07_31_2019 08_07_2019     18.6        86   93.7       32        8
## 2 07_30_2019 08_01_2019 08_08_2019     17.9        66   91.1       33        4
## 3 07_29_2019 07_30_2019 08_05_2019     15.4        UP   77.5       28        8
## 4 07_30_2019 08_01_2019 08_08_2019     19.0        UP   87.6       30        9
## 5 07_30_2019 08_01_2019 08_07_2019     13.5       141   80.2       33        4
## 6       <NA> 07_25_2019 07_31_2019      9.8        UP   54.0       28       11
##   notes
## 1  <NA>
## 2  <NA>
## 3  <NA>
## 4  <NA>
## 5  <NA>
## 6  <NA>
```

Looks like `group` and `condition` are redundant within `row` and `field_ID`. Also `row` is redundant within `field_ID`. 


```r
summary(data)
```

```
##    ï..DNA_ID      field_ID   genotype   group       row         end.    
##  D132   :  1   SH_A_01:  1   elf3:129   A:90   SUN_C  :48   end   : 36  
##  D133   :  1   SH_A_02:  1   WT  :153   B:60   SH_A   :46   middle:250  
##  D134   :  1   SH_A_03:  1   NA's:  4   C:96   SUN_A  :45               
##  D136   :  1   SH_A_04:  1              D:40   SH_C   :42               
##  D137   :  1   SH_A_05:  1                     SH_B   :32               
##  (Other):277   SH_A_06:  1                     SUN_B  :28               
##  NA's   :  4   (Other):280                     (Other):45               
##  condition           germ           yellow         flowering          final    
##  shade:146   06_22_2019:63   07_30_2019: 21   08_15_2019: 17   08_25_2019: 19  
##  sun  :140   06_08_2019:61   08_14_2019: 16   08_17_2019: 16   08_24_2019: 18  
##              06_15_2019:34   08_16_2019: 15   08_01_2019: 15   08_08_2019: 17  
##              06_21_2019:33   08_03_2019: 14   08_18_2019: 14   08_07_2019: 15  
##              06_07_2019:29   07_29_2019: 13   07_30_2019: 13   08_22_2019: 13  
##              (Other)   :64   (Other)   :184   (Other)   :191   (Other)   :172  
##              NA's      : 2   NA's      : 23   NA's      : 20   NA's      : 32  
##     diameter       direction       height          leaf_num    
##  Min.   : 7.00   UP     : 31   Min.   : 54.00   Min.   :26.00  
##  1st Qu.:14.80   65     :  9   1st Qu.: 86.35   1st Qu.:30.00  
##  Median :16.55   32     :  6   Median : 94.35   Median :32.00  
##  Mean   :16.22   59     :  5   Mean   : 96.56   Mean   :32.49  
##  3rd Qu.:18.07   66     :  5   3rd Qu.:105.00   3rd Qu.:35.00  
##  Max.   :25.00   (Other):205   Max.   :135.50   Max.   :43.00  
##  NA's   :40      NA's   : 25   NA's   :56       NA's   :57     
##     ax_heads          notes    
##  Min.   : 0.000   burned :  5  
##  1st Qu.: 2.000   thin   :  5  
##  Median : 4.000   dead   :  3  
##  Mean   : 4.101   ugly   :  3  
##  3rd Qu.: 6.000   bagged :  2  
##  Max.   :12.000   (Other): 13  
##  NA's   :59       NA's   :255
```

```r
data %>% filter(genotype == "elf3") %>% summary()
```

```
##    ï..DNA_ID      field_ID   genotype   group       row         end.    
##  D168   :  1   SH_A_01:  1   elf3:129   A:34   SUN_C  :24   end   : 20  
##  D169   :  1   SH_A_02:  1   WT  :  0   B:26   SH_C   :22   middle:109  
##  D171   :  1   SH_A_03:  1              C:48   SH_A   :17               
##  D172   :  1   SH_A_04:  1              D:21   SUN_A  :17               
##  D173   :  1   SH_A_09:  1                     SH_B   :14               
##  D174   :  1   SH_A_10:  1                     SH_D   :12               
##  (Other):123   (Other):123                     (Other):23               
##  condition          germ           yellow        flowering         final   
##  shade:67   06_21_2019:31   08_16_2019:11   08_17_2019:11   08_25_2019:15  
##  sun  :62   06_07_2019:28   08_15_2019: 8   08_03_2019:10   08_24_2019:14  
##             06_14_2019:21   08_17_2019: 8   08_18_2019:10   08_08_2019: 7  
##             06_22_2019:17   07_31_2019: 7   08_20_2019: 7   08_09_2019: 6  
##             07_2019_03: 7   08_01_2019: 6   08_15_2019: 6   08_11_2019: 5  
##             06_08_2019: 6   (Other)   :81   (Other)   :78   (Other)   :68  
##             (Other)   :19   NA's      : 8   NA's      : 7   NA's      :14  
##     diameter       direction       height         leaf_num        ax_heads    
##  Min.   : 7.00   UP     :  6   Min.   : 77.2   Min.   :28.00   Min.   : 0.00  
##  1st Qu.:15.10   65     :  4   1st Qu.: 89.9   1st Qu.:32.00   1st Qu.: 2.00  
##  Median :16.55   73     :  4   Median : 99.5   Median :34.00   Median : 3.00  
##  Mean   :16.54   80     :  4   Mean   :101.0   Mean   :34.75   Mean   : 3.63  
##  3rd Qu.:18.30   118    :  3   3rd Qu.:110.2   3rd Qu.:37.00   3rd Qu.: 5.00  
##  Max.   :25.00   (Other):100   Max.   :135.5   Max.   :43.00   Max.   :11.00  
##  NA's   :19      NA's   :  8   NA's   :28      NA's   :28      NA's   :29     
##                            notes    
##  burned                       :  2  
##  bagged                       :  1  
##  dead                         :  1  
##  no apical meristem           :  1  
##  small head, thin, head stolen:  1  
##  (Other)                      :  3  
##  NA's                         :120
```

Experimental setup appears to be four planting groups, each with all combinations of genotype (WT | elf3) and condition (sun | shade).

**Does variable parsing make sense? Is data format consistent within variables? Easier ways to parse?**   


```r
str(data)
```

```
## 'data.frame':	286 obs. of  17 variables:
##  $ ï..DNA_ID: Factor w/ 282 levels "D132","D133",..: 1 2 3 4 5 6 7 8 9 10 ...
##  $ field_ID : Factor w/ 286 levels "SH_A_01","SH_A_02",..: 147 148 149 155 156 157 158 163 164 165 ...
##  $ genotype : Factor w/ 2 levels "elf3","WT": 2 2 2 2 2 2 2 2 2 2 ...
##  $ group    : Factor w/ 4 levels "A","B","C","D": 1 1 1 1 1 1 1 1 1 1 ...
##  $ row      : Factor w/ 9 levels "SH_A","SH_B",..: 6 6 6 6 6 6 6 6 6 6 ...
##  $ end.     : Factor w/ 2 levels "end","middle": 1 1 2 2 2 2 2 2 2 2 ...
##  $ condition: Factor w/ 2 levels "shade","sun": 2 2 2 2 2 2 2 2 2 2 ...
##  $ germ     : Factor w/ 10 levels "06_07_2019","06_08_2019",..: 1 2 2 2 2 2 2 2 2 2 ...
##  $ yellow   : Factor w/ 35 levels "07_26_2019","07_27_2019",..: 5 5 4 5 5 NA 2 4 4 4 ...
##  $ flowering: Factor w/ 35 levels "03_28_2019","07_25_2019",..: 5 6 4 6 6 2 3 5 4 4 ...
##  $ final    : Factor w/ 33 levels "07_31_2019","08_04_2019",..: 5 6 3 6 5 1 2 5 4 6 ...
##  $ diameter : num  18.6 17.9 15.4 19 13.5 9.8 16.1 16.8 16.3 19.7 ...
##  $ direction: Factor w/ 119 levels "0","10","101",..: 108 93 119 119 31 119 84 69 28 119 ...
##  $ height   : num  93.7 91.1 77.5 87.6 80.2 54 72.7 87.4 89.2 91 ...
##  $ leaf_num : int  32 33 28 30 33 28 28 28 29 31 ...
##  $ ax_heads : int  8 4 8 9 4 11 8 8 7 6 ...
##  $ notes    : Factor w/ 15 levels "bagged","bottom of stem chewed",..: NA NA NA NA NA NA NA NA NA NA ...
```

Well, dates might be easier to work with when formatted as dates. Also, `direction` appears to have a mix of data formats.
 
**Suggestions for new variables?**    

  * Days to anthesis   
  * Days to flowering   


