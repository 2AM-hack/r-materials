# Example rOpenSci Packages
Martin Fenner  
5. Oktober 2015  

[rOpenSci](https://ropensci.org) provides R packages for scholarly APIs, including altmetrics services.

### alm
A package for the [lagotto](https://github.com/lagotto/lagotto) open source application. The [alm tutorial](https://ropensci.org/tutorials/alm_tutorial.html) is a good starting point.

Install and load the package with 

```r
#install.packages("alm")
library(alm)
```

```
## Warning: package 'alm' was built under R version 3.1.3
```

```
## 
## 
##  New to alm? Tutorial at http://ropensci.org/tutorials/alm_tutorial.html. Use suppressPackageStartupMessages() to suppress these startup messages in the future
```

My default the package talks to the lagotto instance run by the publisher PLOS at `http://alm.plos.org`. You can specify the `url` parameter to talk to a different instance of the Lagotto API, e.g. `http://cls.labs.datacite.org`.

Get metrics for a particular DOI

```r
out <- alm_ids(doi="10.1371/journal.pone.0029797")
out$data
```

```
##                       .id  pdf  html readers comments likes  total
## 1               citeulike    0     0       0        0     0      0
## 2                crossref    0     0       0        0     0      9
## 3                  nature    0     0       0        0     0      4
## 4                  pubmed    0     0       0        0     0      2
## 5                  scopus    0     0       0        0     0     11
## 6                 counter 2654 33846       0        0     0  36629
## 7        researchblogging    0     0       0        0     0      1
## 8                     pmc  103   813       0        0     0    916
## 9                facebook    0     0       4        0     0      4
## 10               mendeley    0     0     108        0     0    108
## 11                twitter    0     0       0       12     0     12
## 12              wikipedia    0     0       0        0     0     64
## 13          scienceseeker    0     0       0        0     0      0
## 14         relativemetric    0     0       0        0     0 243342
## 15                  f1000    0     0       0        0     0      0
## 16               figshare    0    49       0        0     0     49
## 17              pmceurope    0     0       0        0     0      4
## 18          pmceuropedata    0     0       0        0     0     49
## 19            openedition    0     0       0        0     0      0
## 20              wordpress    0     0       0        0     0      0
## 21                 reddit    0     0       0        0     0      0
## 22               datacite    0     0       0        0     0      0
## 23             copernicus    0     0       0        0     0      0
## 24        articlecoverage    0     0       0        0     0      0
## 25 articlecoveragecurated    0     0       0        0     0      0
## 26          plos_comments    0     0       0        0     0     16
## 27                  orcid    0     0       0        0     0      0
```

get metrics for a set of DOIs

```r
dois <- c('10.1371/journal.pone.0001543','10.1371/journal.pone.0040117',
    '10.1371/journal.pone.0029797','10.1371/journal.pone.0039395')
out <- alm_ids(doi=dois)
lapply(out$data, head)
```

```
## $`10.1371/journal.pone.0040117`
##         .id pdf html readers comments likes total
## 1 citeulike   0    0       0        0     0     0
## 2  crossref   0    0       0        0     0    11
## 3    nature   0    0       0        0     0     0
## 4    pubmed   0    0       0        0     0    11
## 5    scopus   0    0       0        0     0    22
## 6   counter 510 2740       0        0     0  3281
## 
## $`10.1371/journal.pone.0039395`
##         .id pdf html readers comments likes total
## 1 citeulike   0    0       0        0     0     0
## 2  crossref   0    0       0        0     0     2
## 3    nature   0    0       0        0     0     0
## 4    pubmed   0    0       0        0     0     2
## 5    scopus   0    0       0        0     0     5
## 6   counter 565 2069       0        0     0  2669
## 
## $`10.1371/journal.pone.0029797`
##         .id  pdf  html readers comments likes total
## 1 citeulike    0     0       0        0     0     0
## 2  crossref    0     0       0        0     0     9
## 3    nature    0     0       0        0     0     4
## 4    pubmed    0     0       0        0     0     2
## 5    scopus    0     0       0        0     0    11
## 6   counter 2654 33846       0        0     0 36629
## 
## $`10.1371/journal.pone.0001543`
##         .id pdf html readers comments likes total
## 1 citeulike   0    0       0        0     0     0
## 2  crossref   0    0       0        0     0     9
## 3    nature   0    0       0        0     0     0
## 4    pubmed   0    0       0        0     0     9
## 5    scopus   0    0       0        0     0    13
## 6   counter 497 3028       0        0     0  3579
```
