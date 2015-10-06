# Starting with data
Najko Jahn  
5. Oktober 2015  

Adapted and re-used from : [Data carpentry -- Starting with R for data analysis](https://github.com/datacarpentry/R-ecology)

# Skills

* Load spreadsheets into R
* Explore the nature of the datasets
* Store data on your local disk

In many cases, you will work with data. R supports several ways of loading datasets. One is to fetch spreadsheets from the web.

## Spreadsheet data

Let's download journal metadata from the Directory of Open Access Jorunals into our data folder by using `curl` methods.


```r
download.file("https://doaj.org/csv", "examplesdoaj.csv", method = "curl")
```

Load the dataset into R console with `read.csv`


```r
doaj <- read.csv(file = "examples/doaj.csv", sep = ",", header = TRUE)
```

Show the first six rows


```r
head(doaj)
```

```
##                              Journal.title
## 1 Anais da Academia Brasileira de Ciências
## 2                                     ACME
## 3                           Acta Adriatica
## 4                 Acta Biochimica Polonica
## 5               Acta Dermato-Venereologica
## 6                Acta Médica Costarricense
##                                                                         Journal.URL
## 1                   http://www.scielo.br/scielo.php?pid=0001-3765&script=sci_serial
## 2                                            http://riviste.unimi.it/index.php/ACME
## 3                                                   http://jadran.izor.hr/acta/eng/
## 4                                                              http://www.actabp.pl
## 5                                                http://www.medicaljournals.se/acta
## 6 http://www.scielo.sa.cr/scielo.php?script=sci_serial&pid=0001-6002&lng=en&nrm=iso
##   Alternative.title Journal.ISSN..print.version.
## 1                                      0001-3765
## 2                                      0001-494X
## 3                                      0001-5113
## 4                                      0001-527X
## 5                                      0001-5555
## 6                                      0001-6012
##   Journal.EISSN..online.version.
## 1                               
## 2                      2282-0035
## 3                      1846-0453
## 4                      1734-154X
## 5                      1651-2057
## 6                               
##                                               Publisher
## 1                       Academia Brasileira de Ciências
## 2                      Università degli Studi di Milano
## 3        Institute of Oceanography and Fisheries, Split
## 4                              Acta Biochimica Polonica
## 5 Society for Publication of Acta Dermato-Venereologica
## 6          Colegio de Médicos y Cirujanos de Costa Rica
##   Society.or.institution
## 1                       
## 2                       
## 3                       
## 4                       
## 5                       
## 6                       
##                              Platform..host.or.aggregator
## 1                                           SciELO Brazil
## 2                                                     OJS
## 3 Institute of Oceanography and Fisheries, Split, Croatia
## 4                                Acta Biochimica Polonica
## 5   Society for Publication of Acta Dermato-Venereologica
## 6                                       SciELO Costa Rica
##   Country.of.publisher Journal.article.processing.charges..APCs.
## 1               Brazil                                          
## 2                Italy                                          
## 3              Croatia                                          
## 4               Poland                                          
## 5               Sweden                                          
## 6           Costa Rica                                          
##   APC.information.URL APC.amount Currency Journal.article.submission.fee
## 1                             NA                                        
## 2                             NA                                        
## 3                             NA                                        
## 4                             NA                                        
## 5                             NA                                        
## 6                             NA                                        
##   Submission.fee.URL Submission.fee.amount Submission.fee.currency
## 1                                       NA                        
## 2                                       NA                        
## 3                                       NA                        
## 4                                       NA                        
## 5                                       NA                        
## 6                                       NA                        
##   Number.of.articles.publish.in.the.last.calendar.year
## 1                                                   NA
## 2                                                   NA
## 3                                                   NA
## 4                                                   NA
## 5                                                   NA
## 6                                                   NA
##   Number.of.articles.information.URL
## 1                                 NA
## 2                                 NA
## 3                                 NA
## 4                                 NA
## 5                                 NA
## 6                                 NA
##   Journal.waiver.policy..for.developing.country.authors.etc.
## 1                                                           
## 2                                                           
## 3                                                           
## 4                                                           
## 5                                                           
## 6                                                           
##   Waiver.policy.information.URL Digital.archiving.policy.or.program.s.
## 1                                                                     
## 2                                                                     
## 3                                                                     
## 4                                                                     
## 5                                                                     
## 6                                                                     
##       Archiving..national.library Archiving..other
## 1                                                 
## 2 Italian National Library (BNCF)                 
## 3                                                 
## 4                                                 
## 5                                                 
## 6                                                 
##        Archiving.infomation.URL Journal.full.text.crawl.permission
## 1                                                                 
## 2 http://www.depositolegale.it/                                Yes
## 3                                                                 
## 4                                                                 
## 5                                                                 
## 6                                                                 
##   Permanent.article.identifiers Article.level.metadata.in.DOAJ
## 1                                                           NA
## 2                      DOI, NBN                             NA
## 3                                                           NA
## 4                                                           NA
## 5                                                           NA
## 6                                                           NA
##   Journal.provides.download.statistics Download.statistics.information.URL
## 1                                                                         
## 2                                       they are only for the site manager
## 3                                                                         
## 4                                                                         
## 5                                                                         
## 6                                                                         
##   First.calendar.year.journal.provided.online.Open.Access.content
## 1                                                            2000
## 2                                                            2014
## 3                                                            2004
## 4                                                            1977
## 5                                                            1998
## 6                                                            2000
##   Full.text.formats
## 1                  
## 2               PDF
## 3                  
## 4                  
## 5                  
## 6                  
##                                                                                      Keywords
## 1                              biological sciences, exact and earth sciences, health sciences
## 2                             Italian literature, classic literature, linguistics, philosophy
## 3                                                marine sciences, Mediterranean, Adriatic Sea
## 4                                                                     chemistry, biochemistry
## 5 sexually transmitted infections, psoriasis, psychodermatology, skin immunology, skin cancer
## 6                                                                             health sciences
##   Full.text.language
## 1                   
## 2            Italian
## 3            English
## 4            English
## 5            English
## 6            English
##                             URL.for.the.Editorial.Board.page
## 1                                                           
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialTeam
## 3                                                           
## 4                                                           
## 5                                                           
## 6                                                           
##      Review.process
## 1                  
## 2 Blind peer review
## 3                  
## 4                  
## 5                  
## 6                  
##                                                     Review.process.information.URL
## 1                                                                                 
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#peerReviewProcess
## 3                                                                                 
## 4                                                                                 
## 5                                                                                 
## 6                                                                                 
##                                                 URL.for.journal.s.aims...scope
## 1                                                                             
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#focusAndScope
## 3                                                                             
## 4                                                                             
## 5                                                                             
## 6                                                                             
##                                  URL.for.journal.s.instructions.for.authors
## 1                                                                          
## 2 http://riviste.unimi.it/index.php/ACME/about/submissions#authorGuidelines
## 3                                                                          
## 4                                                                          
## 5                                                                          
## 6                                                                          
##   Journal.plagiarism.screening.policy Plagiarism.information.URL
## 1                                                               
## 2                                                               
## 3                                                               
## 4                                                               
## 5                                                               
## 6                                                               
##   Average.number.of.weeks.between.submission.and.publication
## 1                                                         NA
## 2                                                         12
## 3                                                         NA
## 4                                                         NA
## 5                                                         NA
## 6                                                         NA
##                                           URL.for.journal.s.Open.Access.statement
## 1                                                                                
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#openAccessPolicy
## 3                                                                                
## 4                                                                                
## 5                                                                                
## 6                                                                                
##   Machine.readable.CC.licensing.information.embedded.or.displayed.in.articles
## 1                                                                            
## 2                                                                         Yes
## 3                                                                            
## 4                                                                            
## 5                                                                            
## 6                                                                            
##   URL.to.an.example.page.with.embedded.licensing.information
## 1                                                           
## 2   http://riviste.unimi.it/index.php/ACME/article/view/4280
## 3                                                           
## 4                                                           
## 5                                                           
## 6                                                           
##   Journal.license License.attributes
## 1        CC BY-NC                   
## 2     CC BY-NC-ND                   
## 3                                   
## 4                                   
## 5                                   
## 6                                   
##                          URL.for.license.terms
## 1                                             
## 2 http://riviste.unimi.it/index.php/ACME/index
## 3                                             
## 4                                             
## 5                                             
## 6                                             
##   Does.this.journal.allow.unrestricted.reuse.in.compliance.with.BOAI.
## 1                                                                    
## 2                                                                 Yes
## 3                                                                    
## 4                                                                    
## 5                                                                    
## 6                                                                    
##   Deposit.policy.directory Author.holds.copyright.without.restrictions
## 1                                                                     
## 2                                                                 True
## 3                                                                     
## 4                                                                     
## 5                                                                     
## 6                                                                     
##                                                 Copyright.information.URL
## 1                                                                        
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#custom-1
## 3                                                                        
## 4                                                                        
## 5                                                                        
## 6                                                                        
##   Author.holds.publishing.rights.without.restrictions
## 1                                                    
## 2                                                True
## 3                                                    
## 4                                                    
## 5                                                    
## 6                                                    
##                                          Publishing.rights.information.URL
## 1                                                                         
## 2 http://riviste.unimi.it/index.php/ACME/about/submissions#copyrightNotice
## 3                                                                         
## 4                                                                         
## 5                                                                         
## 6                                                                         
##   DOAJ.Seal Tick..Accepted.after.March.2014        Added.on.Date
## 1        No                              No 2004-04-23T21:31:00Z
## 2        No                             Yes 2014-12-22T19:55:58Z
## 3        No                              No 2006-11-17T17:19:25Z
## 4        No                              No 2003-12-16T00:00:00Z
## 5        No                              No 2011-11-10T12:31:05Z
## 6        No                              No 2004-04-23T21:31:01Z
##                                              Subjects Content.in.DOAJ
## 1                          Science, Biology (General)             Yes
## 2                                       General Works             Yes
## 3   Oceanography, Geography. Anthropology. Recreation             Yes
## 4 Biochemistry, Organic chemistry, Chemistry, Science             Yes
## 5                               Dermatology, Medicine             Yes
## 6                        Medicine, Medicine (General)             Yes
```

How many rows and columns has the dataset?


```r
dim(doaj)
```

```
## [1] 10579    59
```

Show the column names


```r
names(doaj)
```

```
##  [1] "Journal.title"                                                              
##  [2] "Journal.URL"                                                                
##  [3] "Alternative.title"                                                          
##  [4] "Journal.ISSN..print.version."                                               
##  [5] "Journal.EISSN..online.version."                                             
##  [6] "Publisher"                                                                  
##  [7] "Society.or.institution"                                                     
##  [8] "Platform..host.or.aggregator"                                               
##  [9] "Country.of.publisher"                                                       
## [10] "Journal.article.processing.charges..APCs."                                  
## [11] "APC.information.URL"                                                        
## [12] "APC.amount"                                                                 
## [13] "Currency"                                                                   
## [14] "Journal.article.submission.fee"                                             
## [15] "Submission.fee.URL"                                                         
## [16] "Submission.fee.amount"                                                      
## [17] "Submission.fee.currency"                                                    
## [18] "Number.of.articles.publish.in.the.last.calendar.year"                       
## [19] "Number.of.articles.information.URL"                                         
## [20] "Journal.waiver.policy..for.developing.country.authors.etc."                 
## [21] "Waiver.policy.information.URL"                                              
## [22] "Digital.archiving.policy.or.program.s."                                     
## [23] "Archiving..national.library"                                                
## [24] "Archiving..other"                                                           
## [25] "Archiving.infomation.URL"                                                   
## [26] "Journal.full.text.crawl.permission"                                         
## [27] "Permanent.article.identifiers"                                              
## [28] "Article.level.metadata.in.DOAJ"                                             
## [29] "Journal.provides.download.statistics"                                       
## [30] "Download.statistics.information.URL"                                        
## [31] "First.calendar.year.journal.provided.online.Open.Access.content"            
## [32] "Full.text.formats"                                                          
## [33] "Keywords"                                                                   
## [34] "Full.text.language"                                                         
## [35] "URL.for.the.Editorial.Board.page"                                           
## [36] "Review.process"                                                             
## [37] "Review.process.information.URL"                                             
## [38] "URL.for.journal.s.aims...scope"                                             
## [39] "URL.for.journal.s.instructions.for.authors"                                 
## [40] "Journal.plagiarism.screening.policy"                                        
## [41] "Plagiarism.information.URL"                                                 
## [42] "Average.number.of.weeks.between.submission.and.publication"                 
## [43] "URL.for.journal.s.Open.Access.statement"                                    
## [44] "Machine.readable.CC.licensing.information.embedded.or.displayed.in.articles"
## [45] "URL.to.an.example.page.with.embedded.licensing.information"                 
## [46] "Journal.license"                                                            
## [47] "License.attributes"                                                         
## [48] "URL.for.license.terms"                                                      
## [49] "Does.this.journal.allow.unrestricted.reuse.in.compliance.with.BOAI."        
## [50] "Deposit.policy.directory"                                                   
## [51] "Author.holds.copyright.without.restrictions"                                
## [52] "Copyright.information.URL"                                                  
## [53] "Author.holds.publishing.rights.without.restrictions"                        
## [54] "Publishing.rights.information.URL"                                          
## [55] "DOAJ.Seal"                                                                  
## [56] "Tick..Accepted.after.March.2014"                                            
## [57] "Added.on.Date"                                                              
## [58] "Subjects"                                                                   
## [59] "Content.in.DOAJ"
```

To compactly display the structure of arbitrary R objects use `str`


```r
str(doaj)
```

```
## 'data.frame':	10579 obs. of  59 variables:
##  $ Journal.title                                                              : Factor w/ 10563 levels " European Agrophysical Journal ",..: 532 47 55 62 85 119 131 166 167 188 ...
##  $ Journal.URL                                                                : Factor w/ 10574 levels "http:///www.dentalhypotheses.com",..: 9130 2930 1343 3523 7807 9536 10510 10511 1071 46 ...
##  $ Alternative.title                                                          : Factor w/ 2745 levels ""," "," Experimental Psychology (Russia) ",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ Journal.ISSN..print.version.                                               : Factor w/ 9555 levels "","0001-3765",..: 2 3 4 5 6 7 8 9 10 11 ...
##  $ Journal.EISSN..online.version.                                             : Factor w/ 5020 levels "","0034-7493",..: 1 4027 1407 1031 731 1 4830 2764 1406 1146 ...
##  $ Publisher                                                                  : Factor w/ 5918 levels "","    Universidade de São Paulo",..: 36 5210 2275 95 4239 1032 3576 3576 5707 5684 ...
##  $ Society.or.institution                                                     : Factor w/ 892 levels "","    Universidade de São Paulo",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ Platform..host.or.aggregator                                               : Factor w/ 3997 levels "","   "," Revista Brasileira de Geografia Física",..: 2696 2323 1518 61 2901 2701 2323 2323 1315 3797 ...
##  $ Country.of.publisher                                                       : Factor w/ 126 levels "","Albania","Algeria",..: 18 58 30 95 111 29 95 95 30 33 ...
##  $ Journal.article.processing.charges..APCs.                                  : Factor w/ 2 levels "","Yes": 1 1 1 1 1 1 2 1 1 1 ...
##  $ APC.information.URL                                                        : Factor w/ 1370 levels "","hthttp://revistas.urosario.edu.co/index.php/desafios/about/editorialPolicies#openAccessPolicy",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ APC.amount                                                                 : int  NA NA NA NA NA NA 100 NA NA NA ...
##  $ Currency                                                                   : Factor w/ 22 levels "","AUD - Australian Dollar",..: 1 1 1 1 1 1 6 1 1 1 ...
##  $ Journal.article.submission.fee                                             : Factor w/ 2 levels "","Yes": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Submission.fee.URL                                                         : Factor w/ 1363 levels "","http:// http://www.rcommunicationr.org/index.php/about-rcr/aims-scope",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ Submission.fee.amount                                                      : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ Submission.fee.currency                                                    : Factor w/ 12 levels "","BRL - Brazilian Real",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ Number.of.articles.publish.in.the.last.calendar.year                       : logi  NA NA NA NA NA NA ...
##  $ Number.of.articles.information.URL                                         : logi  NA NA NA NA NA NA ...
##  $ Journal.waiver.policy..for.developing.country.authors.etc.                 : Factor w/ 2 levels "","Yes": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Waiver.policy.information.URL                                              : Factor w/ 327 levels "","http://agroaid-bd.org/ralf/publication-fee/",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ Digital.archiving.policy.or.program.s.                                     : Factor w/ 16 levels "","CLOCKSS","CLOCKSS, PMC/Europe PMC/PMC Canada",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ Archiving..national.library                                                : Factor w/ 97 levels ""," Koninklijke Bibliotheek",..: 1 43 1 1 1 1 1 1 1 1 ...
##  $ Archiving..other                                                           : Factor w/ 68 levels ""," Koninklijke Bibliotheek",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ Archiving.infomation.URL                                                   : Factor w/ 875 levels "","http://-",..: 1 433 1 1 1 1 1 1 1 1 ...
##  $ Journal.full.text.crawl.permission                                         : Factor w/ 2 levels "","Yes": 1 2 1 1 1 1 2 1 1 1 ...
##  $ Permanent.article.identifiers                                              : Factor w/ 28 levels "","ARK","Digital Commons Network",..: 1 10 1 1 1 1 4 1 1 1 ...
##  $ Article.level.metadata.in.DOAJ                                             : logi  NA NA NA NA NA NA ...
##  $ Journal.provides.download.statistics                                       : Factor w/ 2 levels "","Yes": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Download.statistics.information.URL                                        : Factor w/ 575 levels ""," http://www.aisthema.eu/ojs/index.php/Aisthema/about/statistics",..: 1 558 1 1 1 1 1 1 1 1 ...
##  $ First.calendar.year.journal.provided.online.Open.Access.content            : int  2000 2014 2004 1977 1998 2000 2006 1990 2000 1999 ...
##  $ Full.text.formats                                                          : Factor w/ 28 levels "","HTML","HTML, ePUB",..: 1 5 1 1 1 1 5 1 1 1 ...
##  $ Keywords                                                                   : Factor w/ 9497 levels "\"Atmospheric Sciences and Ocean Sciences, Biogeosciences",..: 1007 4959 5621 1497 8167 4051 6363 1185 2322 9320 ...
##  $ Full.text.language                                                         : Factor w/ 389 levels "","Abkhazian, English",..: 1 278 72 72 72 72 72 72 49 1 ...
##  $ URL.for.the.Editorial.Board.page                                           : Factor w/ 1932 levels "","http://201.20.109.36:2627/index.php/medicina/about/editorialTeam",..: 1 683 1 1 1 1 1899 1 1 1 ...
##  $ Review.process                                                             : Factor w/ 6 levels "","Blind peer review",..: 1 2 1 1 1 1 3 1 1 1 ...
##  $ Review.process.information.URL                                             : Factor w/ 1910 levels "","http://201.20.109.36:2627/index.php/medicina/about/editorialPolicies",..: 1 692 1 1 1 1 1884 1 1 1 ...
##  $ URL.for.journal.s.aims...scope                                             : Factor w/ 1931 levels "","http://201.20.109.36:2627/index.php/medicina/about/editorialPolicies",..: 1 686 1 1 1 1 1901 1 1 1 ...
##  $ URL.for.journal.s.instructions.for.authors                                 : Factor w/ 1875 levels "","http://201.20.109.36:2627/index.php/medicina/about/submissions#authorGuidelines",..: 1 688 1 1 1 1 1851 1 1 1 ...
##  $ Journal.plagiarism.screening.policy                                        : Factor w/ 2 levels "","Yes": 1 1 1 1 1 1 2 1 1 1 ...
##  $ Plagiarism.information.URL                                                 : Factor w/ 1082 levels "","http://201.20.109.36:2627/index.php/medicina/about/submissions",..: 1 1 1 1 1 1 1070 1 1 1 ...
##  $ Average.number.of.weeks.between.submission.and.publication                 : int  NA 12 NA NA NA NA 16 NA NA NA ...
##  $ URL.for.journal.s.Open.Access.statement                                    : Factor w/ 1704 levels "","http://10027.indexcopernicus.com/index.php?p=1",..: 1 685 1 1 1 1 1682 1 1 1 ...
##  $ Machine.readable.CC.licensing.information.embedded.or.displayed.in.articles: Factor w/ 2 levels "","Yes": 1 2 1 1 1 1 2 1 1 1 ...
##  $ URL.to.an.example.page.with.embedded.licensing.information                 : Factor w/ 1299 levels "","http:// http://journal.tarbiyahiainib.ac.id/index.php/attalim/oai",..: 1 412 1 1 1 1 1284 1 1 1 ...
##  $ Journal.license                                                            : Factor w/ 16 levels "","any of the six CC licenses",..: 5 6 1 1 1 1 4 4 1 1 ...
##  $ License.attributes                                                         : Factor w/ 8 levels "","Attribution",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ URL.for.license.terms                                                      : Factor w/ 1672 levels "","http://abjs.mums.ac.ir/journal/about",..: 1 664 1 1 1 1 1642 1 1 1 ...
##  $ Does.this.journal.allow.unrestricted.reuse.in.compliance.with.BOAI.        : Factor w/ 2 levels "","Yes": 1 2 1 1 1 1 2 1 1 1 ...
##  $ Deposit.policy.directory                                                   : Factor w/ 57 levels ""," Index Copernicus, Latindex, AATA/BCIN",..: 1 1 1 1 1 1 40 1 1 1 ...
##  $ Author.holds.copyright.without.restrictions                                : Factor w/ 24 levels "","Author Choices",..: 1 22 1 1 1 1 22 1 1 1 ...
##  $ Copyright.information.URL                                                  : Factor w/ 1256 levels "","hhttp://www.annales-geophysicae.net/about/licence_and_copyright.html",..: 1 412 1 1 1 1 1239 1 1 1 ...
##  $ Author.holds.publishing.rights.without.restrictions                        : Factor w/ 48 levels ""," De Gruyter Open allows authors the use of the final published version of an article (publisher PDF) for self-archiving (author"| __truncated__,..: 1 45 1 1 1 1 45 1 1 1 ...
##  $ Publishing.rights.information.URL                                          : Factor w/ 1124 levels "","http://131.220.45.179/ojs/index.php/fsd/about/submissions#authorGuidelines",..: 1 382 1 1 1 1 1107 1 1 1 ...
##  $ DOAJ.Seal                                                                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Tick..Accepted.after.March.2014                                            : Factor w/ 2 levels "No","Yes": 1 2 1 1 1 1 2 1 1 1 ...
##  $ Added.on.Date                                                              : Factor w/ 10003 levels "2002-05-01T20:12:48Z",..: 192 8980 1123 119 5149 193 8565 4760 1283 109 ...
##  $ Subjects                                                                   : Factor w/ 1463 levels "","Accounting. Bookkeeping",..: 1218 428 1069 107 216 945 111 130 881 25 ...
##  $ Content.in.DOAJ                                                            : Factor w/ 1 level "Yes": 1 1 1 1 1 1 1 1 1 1 ...
```

**Task 1**: 
Load in the spreadsheet examples/neuro-scimago.csv.

Based on the output of `str(neuro)`, can you answer the following questions?**

* What is the class of the object `neuro`?
* How many different publishers does the Directory of Open Access Journals spreadsheet contain?


## Working with empty cells

Empty cells often affect your analysis. R discriminate missing values with `NA`


```r
x <- c(2:20, NA)
mean(x)
```

```
## [1] NA
```

```r
mean(x, na.rm = TRUE)
```

```
## [1] 11
```

As you have may noticed, the `doaj` dataset has empty cells not designated as `NA`


```r
head(doaj)
```

```
##                              Journal.title
## 1 Anais da Academia Brasileira de Ciências
## 2                                     ACME
## 3                           Acta Adriatica
## 4                 Acta Biochimica Polonica
## 5               Acta Dermato-Venereologica
## 6                Acta Médica Costarricense
##                                                                         Journal.URL
## 1                   http://www.scielo.br/scielo.php?pid=0001-3765&script=sci_serial
## 2                                            http://riviste.unimi.it/index.php/ACME
## 3                                                   http://jadran.izor.hr/acta/eng/
## 4                                                              http://www.actabp.pl
## 5                                                http://www.medicaljournals.se/acta
## 6 http://www.scielo.sa.cr/scielo.php?script=sci_serial&pid=0001-6002&lng=en&nrm=iso
##   Alternative.title Journal.ISSN..print.version.
## 1                                      0001-3765
## 2                                      0001-494X
## 3                                      0001-5113
## 4                                      0001-527X
## 5                                      0001-5555
## 6                                      0001-6012
##   Journal.EISSN..online.version.
## 1                               
## 2                      2282-0035
## 3                      1846-0453
## 4                      1734-154X
## 5                      1651-2057
## 6                               
##                                               Publisher
## 1                       Academia Brasileira de Ciências
## 2                      Università degli Studi di Milano
## 3        Institute of Oceanography and Fisheries, Split
## 4                              Acta Biochimica Polonica
## 5 Society for Publication of Acta Dermato-Venereologica
## 6          Colegio de Médicos y Cirujanos de Costa Rica
##   Society.or.institution
## 1                       
## 2                       
## 3                       
## 4                       
## 5                       
## 6                       
##                              Platform..host.or.aggregator
## 1                                           SciELO Brazil
## 2                                                     OJS
## 3 Institute of Oceanography and Fisheries, Split, Croatia
## 4                                Acta Biochimica Polonica
## 5   Society for Publication of Acta Dermato-Venereologica
## 6                                       SciELO Costa Rica
##   Country.of.publisher Journal.article.processing.charges..APCs.
## 1               Brazil                                          
## 2                Italy                                          
## 3              Croatia                                          
## 4               Poland                                          
## 5               Sweden                                          
## 6           Costa Rica                                          
##   APC.information.URL APC.amount Currency Journal.article.submission.fee
## 1                             NA                                        
## 2                             NA                                        
## 3                             NA                                        
## 4                             NA                                        
## 5                             NA                                        
## 6                             NA                                        
##   Submission.fee.URL Submission.fee.amount Submission.fee.currency
## 1                                       NA                        
## 2                                       NA                        
## 3                                       NA                        
## 4                                       NA                        
## 5                                       NA                        
## 6                                       NA                        
##   Number.of.articles.publish.in.the.last.calendar.year
## 1                                                   NA
## 2                                                   NA
## 3                                                   NA
## 4                                                   NA
## 5                                                   NA
## 6                                                   NA
##   Number.of.articles.information.URL
## 1                                 NA
## 2                                 NA
## 3                                 NA
## 4                                 NA
## 5                                 NA
## 6                                 NA
##   Journal.waiver.policy..for.developing.country.authors.etc.
## 1                                                           
## 2                                                           
## 3                                                           
## 4                                                           
## 5                                                           
## 6                                                           
##   Waiver.policy.information.URL Digital.archiving.policy.or.program.s.
## 1                                                                     
## 2                                                                     
## 3                                                                     
## 4                                                                     
## 5                                                                     
## 6                                                                     
##       Archiving..national.library Archiving..other
## 1                                                 
## 2 Italian National Library (BNCF)                 
## 3                                                 
## 4                                                 
## 5                                                 
## 6                                                 
##        Archiving.infomation.URL Journal.full.text.crawl.permission
## 1                                                                 
## 2 http://www.depositolegale.it/                                Yes
## 3                                                                 
## 4                                                                 
## 5                                                                 
## 6                                                                 
##   Permanent.article.identifiers Article.level.metadata.in.DOAJ
## 1                                                           NA
## 2                      DOI, NBN                             NA
## 3                                                           NA
## 4                                                           NA
## 5                                                           NA
## 6                                                           NA
##   Journal.provides.download.statistics Download.statistics.information.URL
## 1                                                                         
## 2                                       they are only for the site manager
## 3                                                                         
## 4                                                                         
## 5                                                                         
## 6                                                                         
##   First.calendar.year.journal.provided.online.Open.Access.content
## 1                                                            2000
## 2                                                            2014
## 3                                                            2004
## 4                                                            1977
## 5                                                            1998
## 6                                                            2000
##   Full.text.formats
## 1                  
## 2               PDF
## 3                  
## 4                  
## 5                  
## 6                  
##                                                                                      Keywords
## 1                              biological sciences, exact and earth sciences, health sciences
## 2                             Italian literature, classic literature, linguistics, philosophy
## 3                                                marine sciences, Mediterranean, Adriatic Sea
## 4                                                                     chemistry, biochemistry
## 5 sexually transmitted infections, psoriasis, psychodermatology, skin immunology, skin cancer
## 6                                                                             health sciences
##   Full.text.language
## 1                   
## 2            Italian
## 3            English
## 4            English
## 5            English
## 6            English
##                             URL.for.the.Editorial.Board.page
## 1                                                           
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialTeam
## 3                                                           
## 4                                                           
## 5                                                           
## 6                                                           
##      Review.process
## 1                  
## 2 Blind peer review
## 3                  
## 4                  
## 5                  
## 6                  
##                                                     Review.process.information.URL
## 1                                                                                 
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#peerReviewProcess
## 3                                                                                 
## 4                                                                                 
## 5                                                                                 
## 6                                                                                 
##                                                 URL.for.journal.s.aims...scope
## 1                                                                             
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#focusAndScope
## 3                                                                             
## 4                                                                             
## 5                                                                             
## 6                                                                             
##                                  URL.for.journal.s.instructions.for.authors
## 1                                                                          
## 2 http://riviste.unimi.it/index.php/ACME/about/submissions#authorGuidelines
## 3                                                                          
## 4                                                                          
## 5                                                                          
## 6                                                                          
##   Journal.plagiarism.screening.policy Plagiarism.information.URL
## 1                                                               
## 2                                                               
## 3                                                               
## 4                                                               
## 5                                                               
## 6                                                               
##   Average.number.of.weeks.between.submission.and.publication
## 1                                                         NA
## 2                                                         12
## 3                                                         NA
## 4                                                         NA
## 5                                                         NA
## 6                                                         NA
##                                           URL.for.journal.s.Open.Access.statement
## 1                                                                                
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#openAccessPolicy
## 3                                                                                
## 4                                                                                
## 5                                                                                
## 6                                                                                
##   Machine.readable.CC.licensing.information.embedded.or.displayed.in.articles
## 1                                                                            
## 2                                                                         Yes
## 3                                                                            
## 4                                                                            
## 5                                                                            
## 6                                                                            
##   URL.to.an.example.page.with.embedded.licensing.information
## 1                                                           
## 2   http://riviste.unimi.it/index.php/ACME/article/view/4280
## 3                                                           
## 4                                                           
## 5                                                           
## 6                                                           
##   Journal.license License.attributes
## 1        CC BY-NC                   
## 2     CC BY-NC-ND                   
## 3                                   
## 4                                   
## 5                                   
## 6                                   
##                          URL.for.license.terms
## 1                                             
## 2 http://riviste.unimi.it/index.php/ACME/index
## 3                                             
## 4                                             
## 5                                             
## 6                                             
##   Does.this.journal.allow.unrestricted.reuse.in.compliance.with.BOAI.
## 1                                                                    
## 2                                                                 Yes
## 3                                                                    
## 4                                                                    
## 5                                                                    
## 6                                                                    
##   Deposit.policy.directory Author.holds.copyright.without.restrictions
## 1                                                                     
## 2                                                                 True
## 3                                                                     
## 4                                                                     
## 5                                                                     
## 6                                                                     
##                                                 Copyright.information.URL
## 1                                                                        
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#custom-1
## 3                                                                        
## 4                                                                        
## 5                                                                        
## 6                                                                        
##   Author.holds.publishing.rights.without.restrictions
## 1                                                    
## 2                                                True
## 3                                                    
## 4                                                    
## 5                                                    
## 6                                                    
##                                          Publishing.rights.information.URL
## 1                                                                         
## 2 http://riviste.unimi.it/index.php/ACME/about/submissions#copyrightNotice
## 3                                                                         
## 4                                                                         
## 5                                                                         
## 6                                                                         
##   DOAJ.Seal Tick..Accepted.after.March.2014        Added.on.Date
## 1        No                              No 2004-04-23T21:31:00Z
## 2        No                             Yes 2014-12-22T19:55:58Z
## 3        No                              No 2006-11-17T17:19:25Z
## 4        No                              No 2003-12-16T00:00:00Z
## 5        No                              No 2011-11-10T12:31:05Z
## 6        No                              No 2004-04-23T21:31:01Z
##                                              Subjects Content.in.DOAJ
## 1                          Science, Biology (General)             Yes
## 2                                       General Works             Yes
## 3   Oceanography, Geography. Anthropology. Recreation             Yes
## 4 Biochemistry, Organic chemistry, Chemistry, Science             Yes
## 5                               Dermatology, Medicine             Yes
## 6                        Medicine, Medicine (General)             Yes
```

To take care that empty cells are corectly loaded into R, use the `na.strings` option


```r
doaj <- read.csv(file = "examples/doaj.csv", sep = ",", header = TRUE, na.strings = "")
head(doaj)
```

```
##                              Journal.title
## 1 Anais da Academia Brasileira de Ciências
## 2                                     ACME
## 3                           Acta Adriatica
## 4                 Acta Biochimica Polonica
## 5               Acta Dermato-Venereologica
## 6                Acta Médica Costarricense
##                                                                         Journal.URL
## 1                   http://www.scielo.br/scielo.php?pid=0001-3765&script=sci_serial
## 2                                            http://riviste.unimi.it/index.php/ACME
## 3                                                   http://jadran.izor.hr/acta/eng/
## 4                                                              http://www.actabp.pl
## 5                                                http://www.medicaljournals.se/acta
## 6 http://www.scielo.sa.cr/scielo.php?script=sci_serial&pid=0001-6002&lng=en&nrm=iso
##   Alternative.title Journal.ISSN..print.version.
## 1              <NA>                    0001-3765
## 2              <NA>                    0001-494X
## 3              <NA>                    0001-5113
## 4              <NA>                    0001-527X
## 5              <NA>                    0001-5555
## 6              <NA>                    0001-6012
##   Journal.EISSN..online.version.
## 1                           <NA>
## 2                      2282-0035
## 3                      1846-0453
## 4                      1734-154X
## 5                      1651-2057
## 6                           <NA>
##                                               Publisher
## 1                       Academia Brasileira de Ciências
## 2                      Università degli Studi di Milano
## 3        Institute of Oceanography and Fisheries, Split
## 4                              Acta Biochimica Polonica
## 5 Society for Publication of Acta Dermato-Venereologica
## 6          Colegio de Médicos y Cirujanos de Costa Rica
##   Society.or.institution
## 1                   <NA>
## 2                   <NA>
## 3                   <NA>
## 4                   <NA>
## 5                   <NA>
## 6                   <NA>
##                              Platform..host.or.aggregator
## 1                                           SciELO Brazil
## 2                                                     OJS
## 3 Institute of Oceanography and Fisheries, Split, Croatia
## 4                                Acta Biochimica Polonica
## 5   Society for Publication of Acta Dermato-Venereologica
## 6                                       SciELO Costa Rica
##   Country.of.publisher Journal.article.processing.charges..APCs.
## 1               Brazil                                      <NA>
## 2                Italy                                      <NA>
## 3              Croatia                                      <NA>
## 4               Poland                                      <NA>
## 5               Sweden                                      <NA>
## 6           Costa Rica                                      <NA>
##   APC.information.URL APC.amount Currency Journal.article.submission.fee
## 1                <NA>         NA     <NA>                           <NA>
## 2                <NA>         NA     <NA>                           <NA>
## 3                <NA>         NA     <NA>                           <NA>
## 4                <NA>         NA     <NA>                           <NA>
## 5                <NA>         NA     <NA>                           <NA>
## 6                <NA>         NA     <NA>                           <NA>
##   Submission.fee.URL Submission.fee.amount Submission.fee.currency
## 1               <NA>                    NA                    <NA>
## 2               <NA>                    NA                    <NA>
## 3               <NA>                    NA                    <NA>
## 4               <NA>                    NA                    <NA>
## 5               <NA>                    NA                    <NA>
## 6               <NA>                    NA                    <NA>
##   Number.of.articles.publish.in.the.last.calendar.year
## 1                                                   NA
## 2                                                   NA
## 3                                                   NA
## 4                                                   NA
## 5                                                   NA
## 6                                                   NA
##   Number.of.articles.information.URL
## 1                                 NA
## 2                                 NA
## 3                                 NA
## 4                                 NA
## 5                                 NA
## 6                                 NA
##   Journal.waiver.policy..for.developing.country.authors.etc.
## 1                                                       <NA>
## 2                                                       <NA>
## 3                                                       <NA>
## 4                                                       <NA>
## 5                                                       <NA>
## 6                                                       <NA>
##   Waiver.policy.information.URL Digital.archiving.policy.or.program.s.
## 1                          <NA>                                   <NA>
## 2                          <NA>                                   <NA>
## 3                          <NA>                                   <NA>
## 4                          <NA>                                   <NA>
## 5                          <NA>                                   <NA>
## 6                          <NA>                                   <NA>
##       Archiving..national.library Archiving..other
## 1                            <NA>             <NA>
## 2 Italian National Library (BNCF)             <NA>
## 3                            <NA>             <NA>
## 4                            <NA>             <NA>
## 5                            <NA>             <NA>
## 6                            <NA>             <NA>
##        Archiving.infomation.URL Journal.full.text.crawl.permission
## 1                          <NA>                               <NA>
## 2 http://www.depositolegale.it/                                Yes
## 3                          <NA>                               <NA>
## 4                          <NA>                               <NA>
## 5                          <NA>                               <NA>
## 6                          <NA>                               <NA>
##   Permanent.article.identifiers Article.level.metadata.in.DOAJ
## 1                          <NA>                             NA
## 2                      DOI, NBN                             NA
## 3                          <NA>                             NA
## 4                          <NA>                             NA
## 5                          <NA>                             NA
## 6                          <NA>                             NA
##   Journal.provides.download.statistics Download.statistics.information.URL
## 1                                 <NA>                                <NA>
## 2                                 <NA>  they are only for the site manager
## 3                                 <NA>                                <NA>
## 4                                 <NA>                                <NA>
## 5                                 <NA>                                <NA>
## 6                                 <NA>                                <NA>
##   First.calendar.year.journal.provided.online.Open.Access.content
## 1                                                            2000
## 2                                                            2014
## 3                                                            2004
## 4                                                            1977
## 5                                                            1998
## 6                                                            2000
##   Full.text.formats
## 1              <NA>
## 2               PDF
## 3              <NA>
## 4              <NA>
## 5              <NA>
## 6              <NA>
##                                                                                      Keywords
## 1                              biological sciences, exact and earth sciences, health sciences
## 2                             Italian literature, classic literature, linguistics, philosophy
## 3                                                marine sciences, Mediterranean, Adriatic Sea
## 4                                                                     chemistry, biochemistry
## 5 sexually transmitted infections, psoriasis, psychodermatology, skin immunology, skin cancer
## 6                                                                             health sciences
##   Full.text.language
## 1               <NA>
## 2            Italian
## 3            English
## 4            English
## 5            English
## 6            English
##                             URL.for.the.Editorial.Board.page
## 1                                                       <NA>
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialTeam
## 3                                                       <NA>
## 4                                                       <NA>
## 5                                                       <NA>
## 6                                                       <NA>
##      Review.process
## 1              <NA>
## 2 Blind peer review
## 3              <NA>
## 4              <NA>
## 5              <NA>
## 6              <NA>
##                                                     Review.process.information.URL
## 1                                                                             <NA>
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#peerReviewProcess
## 3                                                                             <NA>
## 4                                                                             <NA>
## 5                                                                             <NA>
## 6                                                                             <NA>
##                                                 URL.for.journal.s.aims...scope
## 1                                                                         <NA>
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#focusAndScope
## 3                                                                         <NA>
## 4                                                                         <NA>
## 5                                                                         <NA>
## 6                                                                         <NA>
##                                  URL.for.journal.s.instructions.for.authors
## 1                                                                      <NA>
## 2 http://riviste.unimi.it/index.php/ACME/about/submissions#authorGuidelines
## 3                                                                      <NA>
## 4                                                                      <NA>
## 5                                                                      <NA>
## 6                                                                      <NA>
##   Journal.plagiarism.screening.policy Plagiarism.information.URL
## 1                                <NA>                       <NA>
## 2                                <NA>                       <NA>
## 3                                <NA>                       <NA>
## 4                                <NA>                       <NA>
## 5                                <NA>                       <NA>
## 6                                <NA>                       <NA>
##   Average.number.of.weeks.between.submission.and.publication
## 1                                                         NA
## 2                                                         12
## 3                                                         NA
## 4                                                         NA
## 5                                                         NA
## 6                                                         NA
##                                           URL.for.journal.s.Open.Access.statement
## 1                                                                            <NA>
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#openAccessPolicy
## 3                                                                            <NA>
## 4                                                                            <NA>
## 5                                                                            <NA>
## 6                                                                            <NA>
##   Machine.readable.CC.licensing.information.embedded.or.displayed.in.articles
## 1                                                                        <NA>
## 2                                                                         Yes
## 3                                                                        <NA>
## 4                                                                        <NA>
## 5                                                                        <NA>
## 6                                                                        <NA>
##   URL.to.an.example.page.with.embedded.licensing.information
## 1                                                       <NA>
## 2   http://riviste.unimi.it/index.php/ACME/article/view/4280
## 3                                                       <NA>
## 4                                                       <NA>
## 5                                                       <NA>
## 6                                                       <NA>
##   Journal.license License.attributes
## 1        CC BY-NC               <NA>
## 2     CC BY-NC-ND               <NA>
## 3            <NA>               <NA>
## 4            <NA>               <NA>
## 5            <NA>               <NA>
## 6            <NA>               <NA>
##                          URL.for.license.terms
## 1                                         <NA>
## 2 http://riviste.unimi.it/index.php/ACME/index
## 3                                         <NA>
## 4                                         <NA>
## 5                                         <NA>
## 6                                         <NA>
##   Does.this.journal.allow.unrestricted.reuse.in.compliance.with.BOAI.
## 1                                                                <NA>
## 2                                                                 Yes
## 3                                                                <NA>
## 4                                                                <NA>
## 5                                                                <NA>
## 6                                                                <NA>
##   Deposit.policy.directory Author.holds.copyright.without.restrictions
## 1                     <NA>                                        <NA>
## 2                     <NA>                                        True
## 3                     <NA>                                        <NA>
## 4                     <NA>                                        <NA>
## 5                     <NA>                                        <NA>
## 6                     <NA>                                        <NA>
##                                                 Copyright.information.URL
## 1                                                                    <NA>
## 2 http://riviste.unimi.it/index.php/ACME/about/editorialPolicies#custom-1
## 3                                                                    <NA>
## 4                                                                    <NA>
## 5                                                                    <NA>
## 6                                                                    <NA>
##   Author.holds.publishing.rights.without.restrictions
## 1                                                <NA>
## 2                                                True
## 3                                                <NA>
## 4                                                <NA>
## 5                                                <NA>
## 6                                                <NA>
##                                          Publishing.rights.information.URL
## 1                                                                     <NA>
## 2 http://riviste.unimi.it/index.php/ACME/about/submissions#copyrightNotice
## 3                                                                     <NA>
## 4                                                                     <NA>
## 5                                                                     <NA>
## 6                                                                     <NA>
##   DOAJ.Seal Tick..Accepted.after.March.2014        Added.on.Date
## 1        No                              No 2004-04-23T21:31:00Z
## 2        No                             Yes 2014-12-22T19:55:58Z
## 3        No                              No 2006-11-17T17:19:25Z
## 4        No                              No 2003-12-16T00:00:00Z
## 5        No                              No 2011-11-10T12:31:05Z
## 6        No                              No 2004-04-23T21:31:01Z
##                                              Subjects Content.in.DOAJ
## 1                          Science, Biology (General)             Yes
## 2                                       General Works             Yes
## 3   Oceanography, Geography. Anthropology. Recreation             Yes
## 4 Biochemistry, Organic chemistry, Chemistry, Science             Yes
## 5                               Dermatology, Medicine             Yes
## 6                        Medicine, Medicine (General)             Yes
```

## Saving datasets

To print your data to a `csv` file, use the `write.csv` command.


```r
write.csv(doaj, file = "examples/backup-doaj.csv")
```



