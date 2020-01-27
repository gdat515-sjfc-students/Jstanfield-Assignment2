\#Question:

How have Disney’s mergers and acquisitions of major properties affected
or not affected the stock price?

\#Data

Data from:
<https://finance.yahoo.com/quote/DIS/history?period1=946684800&period2=1580083200&interval=1wk&filter=history&frequency=1wk>

Great site for easy stock
data.

\#GGPLOT2

``` r
fread(file = "C:/Users/Richard/Documents/Data Science/GDAT515/Jstanfield-Assignment2/DIS.csv") -> dis

str(dis)
```

    ## Classes 'data.table' and 'data.frame':   241 obs. of  7 variables:
    ##  $ Date     : chr  "1/1/2000" "2/1/2000" "3/1/2000" "4/1/2000" ...
    ##  $ Open     : num  28.9 35.8 33.5 40.7 43 ...
    ##  $ High     : num  37.5 38.5 41.9 43 43.3 ...
    ##  $ Low      : num  28.4 30.6 32.6 36.6 37.7 ...
    ##  $ Close    : num  35.8 33.5 40.7 43 41.6 ...
    ##  $ Adj Close: num  28.1 26.3 31.9 33.7 32.6 ...
    ##  $ Volume   : int  247071300 144199000 185072200 111136500 110547100 87971600 86321800 103292800 69093100 112361000 ...
    ##  - attr(*, ".internal.selfref")=<externalptr>

``` r
dis %>%
  select(Date, Open) -> dis.data

as.Date(dis.data$Date, "%m/%d/%Y") -> dis.data$Date

str(dis.data)
```

    ## Classes 'data.table' and 'data.frame':   241 obs. of  2 variables:
    ##  $ Date: Date, format: "2000-01-01" "2000-02-01" ...
    ##  $ Open: num  28.9 35.8 33.5 40.7 43 ...
    ##  - attr(*, ".internal.selfref")=<externalptr>

![

``` r
bought <- dis.data %>%
  filter(Date == "2006-02-01" | Date == "2010-01-01" | Date == "2012-12-01" | Date == "2019-04-01")

ggplot(data = dis.data, mapping = aes(x = Date, y = Open)) +
  geom_point() +
  geom_point(data = bought, aes(x = Date, y = Open), color = 'green', size = 5) +
  geom_smooth(method = loess, color = "blue") +
  ggtitle("Disney Stock Open per Month") +
  labs(caption = "The Open Stock Price for Disney each month since 2000. The purchases of Pixar, Marvel, Lucasfilm, and Fox are highlighted.")
```
]
![](Jstanfield-Assignment2_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

Looking at the highlighted points of Disney’s recent major acquisitions,
we can see that each is followed by a notable climb in stock open price,
some more dramatic than others. We can see a very strong and continuing
climb following the purchase of Marvel.
