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
## NULL
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
## 6   counter 510 2742       0        0     0  3283
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
## 6   counter 2654 33850       0        0     0 36633
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

### rcrossref

A package for the CrossRef REST API.

```r
#install.packages("rcrossref")
library(rcrossref)
```

```
## Warning: package 'rcrossref' was built under R version 3.1.3
```

Using DOI content negotiation to get bibtex-formatted metadata.

```r
cat(cr_cn(dois = "10.1126/science.169.3946.635", format = "bibtex"))
```

```
## @article{Frank_1970,
## 	doi = {10.1126/science.169.3946.635},
## 	url = {http://dx.doi.org/10.1126/science.169.3946.635},
## 	year = 1970,
## 	month = {aug},
## 	publisher = {American Association for the Advancement of Science ({AAAS})},
## 	volume = {169},
## 	number = {3946},
## 	pages = {635--641},
## 	author = {H. S. Frank},
## 	title = {The Structure of Ordinary Water: New data and interpretations are yielding new insights into this fascinating substance},
## 	journal = {Science}
## }
```

DOI content negotiation also works with DataCite DOIs.

```r
cat(cr_cn(dois = "10.6084/M9.FIGSHARE.758498", format = "bibtex"))
```

```
## @data{6075de27-781e-4af1-80bd-3160627c5d0f,
##   doi = {10.6084/M9.FIGSHARE.758498},
##   url = {http://dx.doi.org/10.6084/M9.FIGSHARE.758498},
##   author = {Scott Chamberlain; },
##   publisher = {Figshare},
##   title = {Sea ice cover of Southern pole in April each year from 1979 to 2013},
##   year = {2013}
## }
```

Sometimes we need to know whether a DOI is from CrossRef or DataCite (or another registration agency).

```r
cr_agency(dois = c("10.1126/science.169.3946.635", "10.6084/M9.FIGSHARE.758498"))
```

```
## $`10.1126/science.169.3946.635`
## $`10.1126/science.169.3946.635`$DOI
## [1] "10.1126/science.169.3946.635"
## 
## $`10.1126/science.169.3946.635`$agency
## $`10.1126/science.169.3946.635`$agency$id
## [1] "crossref"
## 
## $`10.1126/science.169.3946.635`$agency$label
## [1] "CrossRef"
## 
## 
## 
## $`10.6084/M9.FIGSHARE.758498`
## $`10.6084/M9.FIGSHARE.758498`$DOI
## [1] "10.6084/m9.figshare.758498"
## 
## $`10.6084/M9.FIGSHARE.758498`$agency
## $`10.6084/M9.FIGSHARE.758498`$agency$id
## [1] "datacite"
## 
## $`10.6084/M9.FIGSHARE.758498`$agency$label
## [1] "DataCite"
```

We can get 50 random DOIs from 2014 with the following:

```r
cr_r(sample = 50, from_pub_date='2014-01-01', until_pub_date='2014-12-31')
```

```
##  [1] "10.1109/ase.2008.33"                       
##  [2] "10.1007/978-3-662-26580-2_2"               
##  [3] "10.1098/rspb.2005.3142"                    
##  [4] "10.1130/2014.1211(07)"                     
##  [5] "10.4028/www.scientific.net/amr.726-731.882"
##  [6] "10.3126/njr.v1i1.6316"                     
##  [7] "10.1121/1.386688"                          
##  [8] "10.1007/s00268-008-9901-5"                 
##  [9] "10.3906/kim-1303-32"                       
## [10] "10.1371/journal.pone.0091796.g003"         
## [11] "10.1007/bf03347162"                        
## [12] "10.1371/journal.pone.0109081.g006"         
## [13] "10.1201/b14695-42"                         
## [14] "10.1017/s0031182000023222"                 
## [15] "10.5962/bhl.title.9340"                    
## [16] "10.1016/s1464-2859(00)80045-0"             
## [17] "10.2991/emeit.2012.398"                    
## [18] "10.1016/s0011-9164(06)01182-9"             
## [19] "10.1109/icecs.2000.911467"                 
## [20] "10.2307/2159627"                           
## [21] "10.1016/s0300-9572(96)00998-7"             
## [22] "10.1109/vetec.1996.501514"                 
## [23] "10.1027/1618-3169.52.3.195"                
## [24] "10.1016/j.apergo.2012.07.005"              
## [25] "10.1136/bmj.1.587.344"                     
## [26] "10.1109/62.587055"                         
## [27] "10.1002/chin.200908171"                    
## [28] "10.2139/ssrn.977224"                       
## [29] "10.1039/ct9089301659"                      
## [30] "10.1109/25.350272"                         
## [31] "10.1117/12.264178"                         
## [32] "10.1016/s0957-4166(00)82222-3"             
## [33] "10.1139/e76-066"                           
## [34] "10.1504/ijvas.2011.038177"                 
## [35] "10.1016/j.bbrc.2009.02.138"                
## [36] "10.1180/claymin.1976.011.1.01"             
## [37] "10.1111/j.1467-9345.1967.tb00314.x"        
## [38] "10.1016/s0147-1767(00)00022-5"             
## [39] "10.1002/ecja.4410790205"                   
## [40] "10.1163/1574-9347_bnp_e608640"             
## [41] "10.4000/traduire.460"                      
## [42] "10.1186/isrctn48145465"                    
## [43] "10.3934/dcds.2007.18.627"                  
## [44] "10.1002/prac.18410230131"                  
## [45] "10.1016/0031-9422(93)85263-q"              
## [46] "10.1097/00005392-200205000-00050"          
## [47] "10.1139/o91-126"                           
## [48] "10.1007/bf01430380"                        
## [49] "10.1007/s11005-006-0130-2"                 
## [50] "10.1111/nous.12020"
```
