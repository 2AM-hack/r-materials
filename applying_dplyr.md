# Working with dplyr
Najko Jahn  
5. October 2015  

# Expected outcomes

* Knowledge of dplyr
* Explore journal master files
* Anomyze data
* Merge datasets

# dplyr

`dplyr` is an efficient way to work with data in R. Developed by Hadley Wickham et al. it simplifies working with `data.frames` in R. If you have not installed it yet, get it from CRAN:


```r
install.packages("dplyr")
```


```r
library(dplyr)
```

```
## Warning: package 'dplyr' was built under R version 3.2.2
```

```
## 
## Attaching package: 'dplyr'
## 
## Die folgenden Objekte sind maskiert von 'package:stats':
## 
##     filter, lag
## 
## Die folgenden Objekte sind maskiert von 'package:base':
## 
##     intersect, setdiff, setequal, union
```

The package comes with an [excellent introduction to dplyr](https://cran.r-project.org/web/packages/dplyr/vignettes/introduction.html), which we follow and apply on journal data.

# Load sources

In bibliometrics, you often need to work with journal lists. For instance, using these list you wish to compare journals according to size and impact, or you want to examine, which journals are open access.

Let's start with loading Neuro Science journals from Scimago into R


```r
neuro <- read.csv("examples/neuro_scimago.csv", header = TRUE, sep = ",", dec = ",")
dim(neuro)
```

```
## [1] 509  14
```

```r
head(neuro)
```

```
##   Rank                         Title Type          ISSN    SJR H.index
## 1    1   Nature Reviews Neuroscience    j ISSN 14710048 17.100     283
## 2    2 Annual Review of Neuroscience    k ISSN 15454126 15.637     189
## 3    3           Nature Neuroscience    j ISSN 10976256 10.503     305
## 4    4                        Neuron    j ISSN 08966273 10.229     350
## 5    5  Trends in Cognitive Sciences    j ISSN 1879307X  9.243     202
## 6    6       Trends in Neurosciences    j ISSN 01662236  8.097     229
##   Total.Docs...2014. Total.Docs...3years. Total.Refs. Total.Cites..3years.
## 1                206                  649        9325                 5978
## 2                 25                   75        3210                 1701
## 3                345                  910       10818                11378
## 4                600                 1372       30608                17127
## 5                122                  342        5984                 4171
## 6                 89                  221        7232                 2869
##   Citable.Docs...3years. Cites...Doc...2years. Ref....Doc.        Country
## 1                    199                 28.34       45.27 United Kingdom
## 2                     74                 19.08      128.40  United States
## 3                    824                 13.75       31.36 United Kingdom
## 4                   1304                 11.96       51.01  United States
## 5                    239                 14.06       49.05 United Kingdom
## 6                    208                 12.83       81.26 United Kingdom
```

## Convenience function `tbl_df`

`tbl_df` wraps a local data.frame. 


```r
neuro <- tbl_df(neuro)
neuro
```

```
## Source: local data frame [509 x 14]
## 
##     Rank                                 Title   Type          ISSN    SJR
##    (int)                                (fctr) (fctr)        (fctr)  (dbl)
## 1      1           Nature Reviews Neuroscience      j ISSN 14710048 17.100
## 2      2         Annual Review of Neuroscience      k ISSN 15454126 15.637
## 3      3                   Nature Neuroscience      j ISSN 10976256 10.503
## 4      4                                Neuron      j ISSN 08966273 10.229
## 5      5          Trends in Cognitive Sciences      j ISSN 1879307X  9.243
## 6      6               Trends in Neurosciences      j ISSN 01662236  8.097
## 7      7 Biology of Mood and Anxiety Disorders      j ISSN 20455380  7.124
## 8      8                          EMBO Journal      j ISSN 14602075  6.861
## 9      9                  Molecular Psychiatry      j ISSN 14765578  5.930
## 10    10                          PLoS Biology      j ISSN 15457885  5.505
## ..   ...                                   ...    ...           ...    ...
## Variables not shown: H.index (int), Total.Docs...2014. (int),
##   Total.Docs...3years. (int), Total.Refs. (int), Total.Cites..3years.
##   (int), Citable.Docs...3years. (int), Cites...Doc...2years. (dbl),
##   Ref....Doc. (dbl), Country (fctr)
```

## Filter rows

Select journals with H-index higher than 250


```r
filter(neuro, H.index > 250)
```

```
## Source: local data frame [5 x 14]
## 
##    Rank                       Title   Type          ISSN    SJR H.index
##   (int)                      (fctr) (fctr)        (fctr)  (dbl)   (int)
## 1     1 Nature Reviews Neuroscience      j ISSN 14710048 17.100     283
## 2     3         Nature Neuroscience      j ISSN 10976256 10.503     305
## 3     4                      Neuron      j ISSN 08966273 10.229     350
## 4     8                EMBO Journal      j ISSN 14602075  6.861     323
## 5    18     Journal of Neuroscience      j ISSN 15292401  4.364     350
## Variables not shown: Total.Docs...2014. (int), Total.Docs...3years. (int),
##   Total.Refs. (int), Total.Cites..3years. (int), Citable.Docs...3years.
##   (int), Cites...Doc...2years. (dbl), Ref....Doc. (dbl), Country (fctr)
```

Select journals from the United Kingdom with H-index higher than 250


```r
filter(neuro, H.index > 250, Country == "United Kingdom")
```

```
## Source: local data frame [3 x 14]
## 
##    Rank                       Title   Type          ISSN    SJR H.index
##   (int)                      (fctr) (fctr)        (fctr)  (dbl)   (int)
## 1     1 Nature Reviews Neuroscience      j ISSN 14710048 17.100     283
## 2     3         Nature Neuroscience      j ISSN 10976256 10.503     305
## 3     8                EMBO Journal      j ISSN 14602075  6.861     323
## Variables not shown: Total.Docs...2014. (int), Total.Docs...3years. (int),
##   Total.Refs. (int), Total.Cites..3years. (int), Citable.Docs...3years.
##   (int), Cites...Doc...2years. (dbl), Ref....Doc. (dbl), Country (fctr)
```

## Select rows

To select rows by position, use `slice`.


```r
slice(neuro, 5:10)
```

```
## Source: local data frame [6 x 14]
## 
##    Rank                                 Title   Type          ISSN   SJR
##   (int)                                (fctr) (fctr)        (fctr) (dbl)
## 1     5          Trends in Cognitive Sciences      j ISSN 1879307X 9.243
## 2     6               Trends in Neurosciences      j ISSN 01662236 8.097
## 3     7 Biology of Mood and Anxiety Disorders      j ISSN 20455380 7.124
## 4     8                          EMBO Journal      j ISSN 14602075 6.861
## 5     9                  Molecular Psychiatry      j ISSN 14765578 5.930
## 6    10                          PLoS Biology      j ISSN 15457885 5.505
## Variables not shown: H.index (int), Total.Docs...2014. (int),
##   Total.Docs...3years. (int), Total.Refs. (int), Total.Cites..3years.
##   (int), Citable.Docs...3years. (int), Cites...Doc...2years. (dbl),
##   Ref....Doc. (dbl), Country (fctr)
```

## Arrange rows

`arrange` reorders your data and works similar to `filter()`. To arrange rows in descending order,


```r
arrange(neuro, desc(Total.Docs...2014.)) 
```

```
## Source: local data frame [509 x 14]
## 
##     Rank                                          Title   Type
##    (int)                                         (fctr) (fctr)
## 1     18                        Journal of Neuroscience      j
## 2     22                                     NeuroImage      j
## 3     86 Investigative Ophthalmology and Visual Science      j
## 4    168                                 Neurocomputing      j
## 5     28                                         Stroke      j
## 6    371              Journal of Visualized Experiments      j
## 7    140                Frontiers in Human Neuroscience      j
## 8    119                                   Neuroscience      j
## 9    206           Journal of the Neurological Sciences      j
## 10   252                           Neuroscience Letters      j
## ..   ...                                            ...    ...
## Variables not shown: ISSN (fctr), SJR (dbl), H.index (int),
##   Total.Docs...2014. (int), Total.Docs...3years. (int), Total.Refs. (int),
##   Total.Cites..3years. (int), Citable.Docs...3years. (int),
##   Cites...Doc...2years. (dbl), Ref....Doc. (dbl), Country (fctr)
```

Sort by journal title


```r
arrange(neuro, Title)
```

```
## Source: local data frame [509 x 14]
## 
##     Rank                               Title   Type          ISSN   SJR
##    (int)                              (fctr) (fctr)        (fctr) (dbl)
## 1    125           ACS Chemical Neuroscience      j ISSN 19487193 1.461
## 2    408            Acta Biologica Hungarica      j ISSN 02365383 0.232
## 3    453                  Acta Endocrinology      j ISSN 18410987 0.143
## 4    297  Acta Neurobiologiae Experimentalis      j ISSN 00651400 0.691
## 5    233       Acta Neurologica Scandinavica      j ISSN 16000404 0.928
## 6    426          Acta Neurologica Taiwanica      j ISSN 1028768X 0.187
## 7     14               Acta Neuropathologica      j ISSN 14320533 4.790
## 8    385              Acta Neuropsychiatrica      j ISSN 16015215 0.322
## 9    454          Activitas Nervosa Superior      j ISSN 18029698 0.142
## 10   420 Activitas Nervosa Superior Rediviva      j ISSN 13384015 0.200
## ..   ...                                 ...    ...           ...   ...
## Variables not shown: H.index (int), Total.Docs...2014. (int),
##   Total.Docs...3years. (int), Total.Refs. (int), Total.Cites..3years.
##   (int), Citable.Docs...3years. (int), Cites...Doc...2years. (dbl),
##   Ref....Doc. (dbl), Country (fctr)
```


## Select columns with `select()`


```r
select(neuro, Title, ISSN, SJR)
```

```
## Source: local data frame [509 x 3]
## 
##                                    Title          ISSN    SJR
##                                   (fctr)        (fctr)  (dbl)
## 1            Nature Reviews Neuroscience ISSN 14710048 17.100
## 2          Annual Review of Neuroscience ISSN 15454126 15.637
## 3                    Nature Neuroscience ISSN 10976256 10.503
## 4                                 Neuron ISSN 08966273 10.229
## 5           Trends in Cognitive Sciences ISSN 1879307X  9.243
## 6                Trends in Neurosciences ISSN 01662236  8.097
## 7  Biology of Mood and Anxiety Disorders ISSN 20455380  7.124
## 8                           EMBO Journal ISSN 14602075  6.861
## 9                   Molecular Psychiatry ISSN 14765578  5.930
## 10                          PLoS Biology ISSN 15457885  5.505
## ..                                   ...           ...    ...
```

Select between between `Title` and `H.index`.


```r
select(neuro, Title:H.index)
```

```
## Source: local data frame [509 x 5]
## 
##                                    Title   Type          ISSN    SJR
##                                   (fctr) (fctr)        (fctr)  (dbl)
## 1            Nature Reviews Neuroscience      j ISSN 14710048 17.100
## 2          Annual Review of Neuroscience      k ISSN 15454126 15.637
## 3                    Nature Neuroscience      j ISSN 10976256 10.503
## 4                                 Neuron      j ISSN 08966273 10.229
## 5           Trends in Cognitive Sciences      j ISSN 1879307X  9.243
## 6                Trends in Neurosciences      j ISSN 01662236  8.097
## 7  Biology of Mood and Anxiety Disorders      j ISSN 20455380  7.124
## 8                           EMBO Journal      j ISSN 14602075  6.861
## 9                   Molecular Psychiatry      j ISSN 14765578  5.930
## 10                          PLoS Biology      j ISSN 15457885  5.505
## ..                                   ...    ...           ...    ...
## Variables not shown: H.index (int)
```

Exclude column


```r
select(neuro, -ISSN)
```

```
## Source: local data frame [509 x 13]
## 
##     Rank                                 Title   Type    SJR H.index
##    (int)                                (fctr) (fctr)  (dbl)   (int)
## 1      1           Nature Reviews Neuroscience      j 17.100     283
## 2      2         Annual Review of Neuroscience      k 15.637     189
## 3      3                   Nature Neuroscience      j 10.503     305
## 4      4                                Neuron      j 10.229     350
## 5      5          Trends in Cognitive Sciences      j  9.243     202
## 6      6               Trends in Neurosciences      j  8.097     229
## 7      7 Biology of Mood and Anxiety Disorders      j  7.124       2
## 8      8                          EMBO Journal      j  6.861     323
## 9      9                  Molecular Psychiatry      j  5.930     156
## 10    10                          PLoS Biology      j  5.505     169
## ..   ...                                   ...    ...    ...     ...
## Variables not shown: Total.Docs...2014. (int), Total.Docs...3years. (int),
##   Total.Refs. (int), Total.Cites..3years. (int), Citable.Docs...3years.
##   (int), Cites...Doc...2years. (dbl), Ref....Doc. (dbl), Country (fctr)
```

Use helper functions to `select` columns:

* `starts_with()`
* `ends_with()`
* `matches()`
* `contains()`


```r
select(neuro, matches("Docs", ignore.case = TRUE))
```

```
## Source: local data frame [509 x 3]
## 
##    Total.Docs...2014. Total.Docs...3years. Citable.Docs...3years.
##                 (int)                (int)                  (int)
## 1                 206                  649                    199
## 2                  25                   75                     74
## 3                 345                  910                    824
## 4                 600                 1372                   1304
## 5                 122                  342                    239
## 6                  89                  221                    208
## 7                   0                    2                      2
## 8                 277                 1189                   1137
## 9                 279                  527                    363
## 10                276                  805                    770
## ..                ...                  ...                    ...
```

## Create new columns with mutate()

Calculate number of documents, which do not count as `citable`.


```r
neuro <- mutate(neuro,
       discard = Total.Docs...3years. - Citable.Docs...3years.)
sum(neuro$discard)
```

```
## [1] 18768
```

Get decile ranking according to number of documents in the last year


```r
mutate(neuro, 
       ranking_docs = ntile(Total.Docs...2014., 10))
```

```
## Source: local data frame [509 x 16]
## 
##     Rank                                 Title   Type          ISSN    SJR
##    (int)                                (fctr) (fctr)        (fctr)  (dbl)
## 1      1           Nature Reviews Neuroscience      j ISSN 14710048 17.100
## 2      2         Annual Review of Neuroscience      k ISSN 15454126 15.637
## 3      3                   Nature Neuroscience      j ISSN 10976256 10.503
## 4      4                                Neuron      j ISSN 08966273 10.229
## 5      5          Trends in Cognitive Sciences      j ISSN 1879307X  9.243
## 6      6               Trends in Neurosciences      j ISSN 01662236  8.097
## 7      7 Biology of Mood and Anxiety Disorders      j ISSN 20455380  7.124
## 8      8                          EMBO Journal      j ISSN 14602075  6.861
## 9      9                  Molecular Psychiatry      j ISSN 14765578  5.930
## 10    10                          PLoS Biology      j ISSN 15457885  5.505
## ..   ...                                   ...    ...           ...    ...
## Variables not shown: H.index (int), Total.Docs...2014. (int),
##   Total.Docs...3years. (int), Total.Refs. (int), Total.Cites..3years.
##   (int), Citable.Docs...3years. (int), Cites...Doc...2years. (dbl),
##   Ref....Doc. (dbl), Country (fctr), discard (int), ranking_docs (int)
```

Generate random ids


```r
mutate(neuro,
       ids = stringi::stri_rand_strings(nrow(neuro), 8))
```

```
## Source: local data frame [509 x 16]
## 
##     Rank                                 Title   Type          ISSN    SJR
##    (int)                                (fctr) (fctr)        (fctr)  (dbl)
## 1      1           Nature Reviews Neuroscience      j ISSN 14710048 17.100
## 2      2         Annual Review of Neuroscience      k ISSN 15454126 15.637
## 3      3                   Nature Neuroscience      j ISSN 10976256 10.503
## 4      4                                Neuron      j ISSN 08966273 10.229
## 5      5          Trends in Cognitive Sciences      j ISSN 1879307X  9.243
## 6      6               Trends in Neurosciences      j ISSN 01662236  8.097
## 7      7 Biology of Mood and Anxiety Disorders      j ISSN 20455380  7.124
## 8      8                          EMBO Journal      j ISSN 14602075  6.861
## 9      9                  Molecular Psychiatry      j ISSN 14765578  5.930
## 10    10                          PLoS Biology      j ISSN 15457885  5.505
## ..   ...                                   ...    ...           ...    ...
## Variables not shown: H.index (int), Total.Docs...2014. (int),
##   Total.Docs...3years. (int), Total.Refs. (int), Total.Cites..3years.
##   (int), Citable.Docs...3years. (int), Cites...Doc...2years. (dbl),
##   Ref....Doc. (dbl), Country (fctr), discard (int), ids (chr)
```

## Sampling

Use `sample_n()` for a fixed number and `sample_frac()` for a fixed random sample of rows


```r
sample_n(neuro, 10)
```

```
## Source: local data frame [10 x 15]
## 
##     Rank                                              Title   Type
##    (int)                                             (fctr) (fctr)
## 1     94                                Social Neuroscience      j
## 2    257                                  Epilepsy Research      j
## 3     33                                               Glia      j
## 4    325 Journal of Neuroscience, Psychology, and Economics      j
## 5    342               Journal of Mathematical Neuroscience      j
## 6    189                                Psychiatry Research      j
## 7    485             Hot Topics in Neurology and Psychiatry      k
## 8    223                             Frontiers in Neurology      j
## 9    227                                      Neuro-Signals      j
## 10   339          Canadian Journal of Neurological Sciences      j
## Variables not shown: ISSN (fctr), SJR (dbl), H.index (int),
##   Total.Docs...2014. (int), Total.Docs...3years. (int), Total.Refs. (int),
##   Total.Cites..3years. (int), Citable.Docs...3years. (int),
##   Cites...Doc...2years. (dbl), Ref....Doc. (dbl), Country (fctr), discard
##   (int)
```


```r
sample_frac(neuro, 0.25)
```

```
## Source: local data frame [127 x 15]
## 
##     Rank
##    (int)
## 1    462
## 2     96
## 3    459
## 4      1
## 5     69
## 6    301
## 7     65
## 8    119
## 9    251
## 10   222
## ..   ...
## Variables not shown: Title (fctr), Type (fctr), ISSN (fctr), SJR (dbl),
##   H.index (int), Total.Docs...2014. (int), Total.Docs...3years. (int),
##   Total.Refs. (int), Total.Cites..3years. (int), Citable.Docs...3years.
##   (int), Cites...Doc...2years. (dbl), Ref....Doc. (dbl), Country (fctr),
##   discard (int)
```

## Comparing `data.frames`

Let's explore how many of the neuroscience journals indexed in Scimago are listed in the Directory of Open Access journals. For this aim, download the DOAJ master file

### Load DOAJ master file


```r
doaj <- read.csv("examples/doaj.csv", header = TRUE, sep = ",", na.strings = "")
tbl_df(doaj)
```

```
## Source: local data frame [10,579 x 59]
## 
##                               Journal.title
##                                      (fctr)
## 1  Anais da Academia Brasileira de Ciências
## 2                                      ACME
## 3                            Acta Adriatica
## 4                  Acta Biochimica Polonica
## 5                Acta Dermato-Venereologica
## 6                 Acta Médica Costarricense
## 7                           Acta Mycologica
## 8      Acta Societatis Botanicorum Poloniae
## 9               Acta Stomatologica Croatica
## 10                    Acta Veterinaria Brno
## ..                                      ...
## Variables not shown: Journal.URL (fctr), Alternative.title (fctr),
##   Journal.ISSN..print.version. (fctr), Journal.EISSN..online.version.
##   (fctr), Publisher (fctr), Society.or.institution (fctr),
##   Platform..host.or.aggregator (fctr), Country.of.publisher (fctr),
##   Journal.article.processing.charges..APCs. (fctr), APC.information.URL
##   (fctr), APC.amount (int), Currency (fctr),
##   Journal.article.submission.fee (fctr), Submission.fee.URL (fctr),
##   Submission.fee.amount (int), Submission.fee.currency (fctr),
##   Number.of.articles.publish.in.the.last.calendar.year (lgl),
##   Number.of.articles.information.URL (lgl),
##   Journal.waiver.policy..for.developing.country.authors.etc. (fctr),
##   Waiver.policy.information.URL (fctr),
##   Digital.archiving.policy.or.program.s. (fctr),
##   Archiving..national.library (fctr), Archiving..other (fctr),
##   Archiving.infomation.URL (fctr), Journal.full.text.crawl.permission
##   (fctr), Permanent.article.identifiers (fctr),
##   Article.level.metadata.in.DOAJ (lgl),
##   Journal.provides.download.statistics (fctr),
##   Download.statistics.information.URL (fctr),
##   First.calendar.year.journal.provided.online.Open.Access.content (int),
##   Full.text.formats (fctr), Keywords (fctr), Full.text.language (fctr),
##   URL.for.the.Editorial.Board.page (fctr), Review.process (fctr),
##   Review.process.information.URL (fctr), URL.for.journal.s.aims...scope
##   (fctr), URL.for.journal.s.instructions.for.authors (fctr),
##   Journal.plagiarism.screening.policy (fctr), Plagiarism.information.URL
##   (fctr), Average.number.of.weeks.between.submission.and.publication
##   (int), URL.for.journal.s.Open.Access.statement (fctr),
##   Machine.readable.CC.licensing.information.embedded.or.displayed.in.articles
##   (fctr), URL.to.an.example.page.with.embedded.licensing.information
##   (fctr), Journal.license (fctr), License.attributes (fctr),
##   URL.for.license.terms (fctr),
##   Does.this.journal.allow.unrestricted.reuse.in.compliance.with.BOAI.
##   (fctr), Deposit.policy.directory (fctr),
##   Author.holds.copyright.without.restrictions (fctr),
##   Copyright.information.URL (fctr),
##   Author.holds.publishing.rights.without.restrictions (fctr),
##   Publishing.rights.information.URL (fctr), DOAJ.Seal (fctr),
##   Tick..Accepted.after.March.2014 (fctr), Added.on.Date (fctr), Subjects
##   (fctr), Content.in.DOAJ (fctr)
```

### Match by ISSN

The DOAJ master lists contains both `ISSN`and `EISSN`. Let's select only the `Journal.title`, `Journal.ISSN..print.version.`, `Journal.EISSN..online.version.` and `Journal.article.processing.charges..APCs.` columns.


```r
doaj_short <- select(doaj, 
                     Journal.title, 
                     Journal.ISSN..print.version.,
                     Journal.EISSN..online.version.,
                     Journal.article.processing.charges..APCs.)
```

Rename the columns


```r
colnames(doaj_short) <- c("title", "issn", "eissn", "apc")
doaj_short <- tbl_df(doaj_short)
```

### Prepare columns for mergeing

Both, `issn` and `eissn` contain the pattern `-`. However, the ISSN column in our neuro dataset looks different. 


```r
head(doaj_short$issn)
```

```
## [1] 0001-3765 0001-494X 0001-5113 0001-527X 0001-5555 0001-6012
## 9554 Levels: 0001-3765 0001-494X 0001-5113 0001-527X 0001-5555 ... 8755-6839
```

```r
head(neuro$ISSN)
```

```
## [1] ISSN 14710048 ISSN 15454126 ISSN 10976256 ISSN 08966273 ISSN 1879307X
## [6] ISSN 01662236
## 509 Levels:  ISSN 0004282X ISSN 00071161 ISSN 00100277 ... ISSN 868601X
```
  
Let's remove those patterns, which, otherwise, would let our merge fail.


```r
doaj_short <- mutate(doaj_short, 
       issn = gsub("-","",issn), 
       eissn = gsub("-","", eissn)
)

neuro <- mutate(neuro,
                issn = gsub("ISSN ", "", ISSN))
```

Filter rows, which either match `issn` or `eissn`column in the `doaj_short`data frame.


```r
filter(neuro, issn %in% doaj_short$issn | issn %in% doaj_short$eissn)
```

```
## Source: local data frame [95 x 16]
## 
##     Rank                                       Title   Type          ISSN
##    (int)                                      (fctr) (fctr)        (fctr)
## 1      7       Biology of Mood and Anxiety Disorders      j ISSN 20455380
## 2     10                                PLoS Biology      j ISSN 15457885
## 3     11                                       eLife      j ISSN 2050084X
## 4     23                                Open Biology      j ISSN 20462441
## 5     29 Computational Intelligence and Neuroscience      j ISSN 16875273
## 6     31                  PLoS Computational Biology      j ISSN 15537358
## 7     37                 Molecular Neurodegeneration      j ISSN 17501326
## 8     41                    Translational Psychiatry      j ISSN 21583188
## 9     44           DMM Disease Models and Mechanisms      j ISSN 17548411
## 10    46                            Molecular Autism      j ISSN 20402392
## ..   ...                                         ...    ...           ...
## Variables not shown: SJR (dbl), H.index (int), Total.Docs...2014. (int),
##   Total.Docs...3years. (int), Total.Refs. (int), Total.Cites..3years.
##   (int), Citable.Docs...3years. (int), Cites...Doc...2years. (dbl),
##   Ref....Doc. (dbl), Country (fctr), discard (int), issn (chr)
```



