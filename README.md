# Objective

This project aims to analyze Boeing Company (`BA`) stock data from 2007
to 2025 using statistical and visualization techniques. Daily, weekly,
and monthly return patterns were examined, along with comparisons across
different periods and explorations of return distributions.
Kolmogorov-Smirnov tests were applied to identify statistically
significant differences, and various smoothing techniques, including
LOESS, Polynomial Regression, and Generalized Additive Models (GAM),
were used to highlight trends. Stock performance was visualized to
uncover meaningful patterns and market behaviors.

# Data Transformation

## Looking for column names

    colnames(djdata)

    ##  [1] "MMM"  "AXP"  "AMGN" "AMZN" "AAPL" "BA"   "CAT"  "CVX"  "CSCO" "KO"  
    ## [11] "DIS"  "GS"   "HD"   "HON"  "IBM"  "JNJ"  "JPM"  "MCD"  "MRK"  "MSFT"
    ## [21] "NKE"  "NVDA" "PG"   "CRM"  "SHW"  "TRV"  "UNH"  "VZ"   "V"    "WMT"

    colnames(djdata.df)

    ##  [1] "Date" "MMM"  "AXP"  "AMGN" "AMZN" "AAPL" "BA"   "CAT"  "CVX"  "CSCO"
    ## [11] "KO"   "DIS"  "GS"   "HD"   "HON"  "IBM"  "JNJ"  "JPM"  "MCD"  "MRK" 
    ## [21] "MSFT" "NKE"  "NVDA" "PG"   "CRM"  "SHW"  "TRV"  "UNH"  "VZ"   "V"   
    ## [31] "WMT"

When we look at the column names of the data, we can see there is no
uppercase or blank characters. So we don’t have to clean the column
names.

## Removing IBM from data & Selecting BA from data

    symbols <- colnames(djdata)
    symbols

    ##  [1] "MMM"  "AXP"  "AMGN" "AMZN" "AAPL" "BA"   "CAT"  "CVX"  "CSCO" "KO"  
    ## [11] "DIS"  "GS"   "HD"   "HON"  "IBM"  "JNJ"  "JPM"  "MCD"  "MRK"  "MSFT"
    ## [21] "NKE"  "NVDA" "PG"   "CRM"  "SHW"  "TRV"  "UNH"  "VZ"   "V"    "WMT"

    symbols[-15]

    ##  [1] "MMM"  "AXP"  "AMGN" "AMZN" "AAPL" "BA"   "CAT"  "CVX"  "CSCO" "KO"  
    ## [11] "DIS"  "GS"   "HD"   "HON"  "JNJ"  "JPM"  "MCD"  "MRK"  "MSFT" "NKE" 
    ## [21] "NVDA" "PG"   "CRM"  "SHW"  "TRV"  "UNH"  "VZ"   "V"    "WMT"

    set.seed(20022025)
    sample(symbols[-15], 16)

    ##  [1] "JNJ"  "MSFT" "BA"   "AXP"  "AAPL" "HD"   "DIS"  "MMM"  "UNH"  "NKE" 
    ## [11] "AMGN" "MCD"  "TRV"  "VZ"   "GS"   "JPM"

    set.seed(20022025)
    lst <- sample(symbols[-15], 16)

    lst[3]

    ## [1] "BA"

    djdata[,lst[3]]

    ##                   BA
    ## 2007-01-03  64.40572
    ## 2007-01-04  64.66572
    ## 2007-01-05  64.39128
    ## 2007-01-08  64.23962
    ## 2007-01-09  63.56065
    ## 2007-01-10  64.47794
    ## 2007-01-11  64.16737
    ## 2007-01-12  63.65453
    ## 2007-01-16  63.56065
    ## 2007-01-17  64.16013
    ##        ...          
    ## 2025-03-06 158.42999
    ## 2025-03-07 154.17999
    ## 2025-03-10 148.14999
    ## 2025-03-11 154.06000
    ## 2025-03-12 158.80000
    ## 2025-03-13 159.32001
    ## 2025-03-14 161.81000
    ## 2025-03-17 161.85001
    ## 2025-03-18 161.57001
    ## 2025-03-19 172.62000

    getSymbols(lst[3])

    ## [1] "BA"

From here we see that, according to the set seed our stock is `BA`
(Boeing Company).

## Looking for the first and last few observations of data

    head(BA)

    ##            BA.Open BA.High BA.Low BA.Close BA.Volume BA.Adjusted
    ## 2007-01-03   88.90   90.30  88.45    89.17   4871700    64.40574
    ## 2007-01-04   88.34   89.83  87.01    89.53   2718900    64.66575
    ## 2007-01-05   89.78   90.00  88.50    89.15   3285900    64.39128
    ## 2007-01-08   88.61   89.41  87.56    88.94   2989000    64.23963
    ## 2007-01-09   88.93   89.71  87.56    88.00   4193800    63.56068
    ## 2007-01-10   88.04   89.34  88.00    89.27   3955200    64.47794

    tail(BA)

    ##            BA.Open BA.High BA.Low BA.Close BA.Volume BA.Adjusted
    ## 2025-05-16  205.69  206.24 203.02   205.82   8496800      205.82
    ## 2025-05-19  203.00  205.60 202.30   205.25   5740200      205.25
    ## 2025-05-20  205.00  208.62 205.00   207.67   5876000      207.67
    ## 2025-05-21  206.60  207.12 202.43   203.21   6616300      203.21
    ## 2025-05-22  202.53  204.73 201.85   203.41   3634500      203.41
    ## 2025-05-23  199.95  203.20 198.75   202.36   5249600      202.36

From head and tail of the data we can confirm that we imported data
correctly.

# Visual Summaries

## Plot for opening, closing prices, high and low values and the volume

    plot(as.zoo(BA))

![image](https://github.com/user-attachments/assets/cfbf6e4a-fac1-49d2-9c8d-59904263f969)

We see that the `BA.Open`, `BA.High`, `BA.Low`, and `BA.Close` graphs
display stock prices at different points, with clear volatility and a
big drop around 2020. The `BA.Volume` graph highlights trading activity,
with noticeable spikes that likely indicate significant events or
decisions made by investors. The BA.Adjusted graph shows the adjusted
closing prices, which take dividends and stock splits into account,
giving a more accurate picture of value.

## Line Chart (2007 - 2025)

    plot(BA[,-5])

![image](https://github.com/user-attachments/assets/98c28541-da80-4da8-ba09-4c0c7cae752d)

At this line graph we can see that it remains stable until 2016,
followed by a sharp rise peaking in 2019. A sudden drop in 2020 that I
assume its because of the pandemics. After 2021, the values fluctuate
but stabilize at a lower level than the peak.

# Date and Time Analysis in Stock Returns

## Retrieving Weekday Data with and Without Labels

    # First few days without labelling.
    head(wday(index(BA), label=F))

    ## [1] 4 5 6 2 3 4

    # First few days with labelling..
    head(wday(index(BA), label=T))

    ## [1] Çar Per Cum Pzt Sal Çar
    ## Levels: Paz < Pzt < Sal < Çar < Per < Cum < Cmt

## Extracting and Converting Weekday Data

    # result is factor object..
    str(head(wday(index(BA), label=T)))

    ##  Ord.factor w/ 7 levels "Paz"<"Pzt"<"Sal"<..: 4 5 6 2 3 4

    is.factor(head(wday(index(BA), label=T)))

    ## [1] TRUE

    # Get the first few days as character (instead of factor)
    paste(head(wday(index(BA), label=T)))

    ## [1] "Çar" "Per" "Cum" "Pzt" "Sal" "Çar"

## Extracting Time-Based Features from Stock Data

    # days of year
    yday(Sys.Date())

    ## [1] 145

    yday(index(first(BA["200303"], "1 week")))

    ## numeric(0)

    # days of quarter
    qday(Sys.Date())

    ## [1] 55

    head(qday(index(BA)))

    ## [1]  3  4  5  8  9 10

    quarter(Sys.Date()) # quarter of the date

    ## [1] 2

    # days of month
    head(mday(index(BA)))

    ## [1]  3  4  5  8  9 10

    # month of first few obs.
    head(month(index(BA)))

    ## [1] 1 1 1 1 1 1

    # Convert to monthly data using to.monthly() function. Then get the first few months
    head(month(index(to.monthly(BA)), label=T))

    ## [1] Oca Şub Mar Nis May Haz
    ## 12 Levels: Oca < Şub < Mar < Nis < May < Haz < Tem < Ağu < Eyl < ... < Ara

    # Just names only..
    paste(head(month(index(to.monthly(BA)), label=T)))

    ## [1] "Oca" "Şub" "Mar" "Nis" "May" "Haz"

## Last Weekdays of Months

    # last weekdays of months and of course weekdaysdate
    last_weekday_o_month <- function(dx) {
      ave( 
      paste(wday(dx, label=T, abbr=F)), 
      paste(month(dx, label=T, abbr = F)), 
      FUN = function(x) tail(x[ !(x %in% c("Saturday","Sunday")) ], 1) 
      ) 
    }

    last_weekdaydate_o_month <- function(dx){
      ave( 
        dx, 
    # paste(month(dx, label=T, abbr = F)), 
        month(dx, label=T),
        year(dx),
        FUN = function(x) tail(x[ !(wday(x, label=T, abbr=F) %in% c("Saturday","Sunday")) ], 1) 
      )
    }  

    # Get the last 25 end of months weekdays Adjusted close value..
    Ad(BA[tail(unique(last_weekdaydate_o_month(index(BA))), 15),])

    ##            BA.Adjusted
    ## 2024-03-28      192.99
    ## 2024-04-30      167.84
    ## 2024-05-31      177.61
    ## 2024-06-28      182.01
    ## 2024-07-31      190.60
    ## 2024-08-30      173.74
    ## 2024-09-30      152.04
    ## 2024-10-31      149.31
    ## 2024-11-29      155.44
    ## 2024-12-31      177.00
    ## 2025-01-31      176.52
    ## 2025-02-28      174.63
    ## 2025-03-31      170.55
    ## 2025-04-30      183.24
    ## 2025-05-23      202.36

The price started at (`203.72`) in February 2024 but showed a downward
trend over time. After a brief recovery in July 2024 (`190.60`), the
stock declined again, reaching (`149.31`) in October. Although there was
a slight increase at the end of 2024, the price dropped significantly in
early 2025, hitting (`136.59`) in April. This suggests overall
instability, with short-term recoveries but a general downward trend.

## Close, Adjusted Close, Day-of-week

    ba <- Ad(BA)

    # Get Mondays
    head(ba[wday(index(ba))==2])

    ##            BA.Adjusted
    ## 2007-01-08    64.23963
    ## 2007-01-22    61.82719
    ## 2007-01-29    61.75495
    ## 2007-02-05    65.52525
    ## 2007-02-12    64.67622
    ## 2007-02-26    64.48044

    # Mondays.. 
    wday(head(ba[wday(index(ba))==2]), label=T)

    ## [1] Pzt Pzt Pzt Pzt Pzt Pzt
    ## Levels: Paz < Pzt < Sal < Çar < Per < Cum < Cmt

    # Fridays.. 
    wday(head(ba[wday(index(ba))==6]), label=T)

    ## [1] Cum Cum Cum Cum Cum Cum
    ## Levels: Paz < Pzt < Sal < Çar < Per < Cum < Cmt

    # Get return series (cont. compounding, log(xt/xt-1)=log(xt)-log(xt-1))
    ba.ret <- diff(log(ba))

    # Mondays returns..
    head(ba.ret[wday(index(ba.ret))==2])

    ##              BA.Adjusted
    ## 2007-01-08 -0.0023579020
    ## 2007-01-22 -0.0347849675
    ## 2007-01-29  0.0008193024
    ## 2007-02-05  0.0074124913
    ## 2007-02-12 -0.0089287398
    ## 2007-02-26 -0.0150667544

    # Data and return series together..
    head(merge(ba, ba.ret))

    ##            BA.Adjusted BA.Adjusted.1
    ## 2007-01-03    64.40574            NA
    ## 2007-01-04    64.66575   0.004028932
    ## 2007-01-05    64.39128  -0.004253436
    ## 2007-01-08    64.23963  -0.002357902
    ## 2007-01-09    63.56068  -0.010625289
    ## 2007-01-10    64.47794   0.014328038

    # Head of mondays returns with levels.
    head(merge(ba, ba.ret)[wday(merge(ba, ba.ret))==2])

    ##            BA.Adjusted BA.Adjusted.1
    ## 2007-01-08    64.23963 -0.0023579020
    ## 2007-01-22    61.82719 -0.0347849675
    ## 2007-01-29    61.75495  0.0008193024
    ## 2007-02-05    65.52525  0.0074124913
    ## 2007-02-12    64.67622 -0.0089287398
    ## 2007-02-26    64.48044 -0.0150667544

The data presents Boeing’s (`BA`) adjusted stock prices and their
percentage changes over time, starting from January 2007. The
(`BA.Adjusted`) column shows the stock’s adjusted closing prices, while
(`BA.Adjusted`).1 represents the percentage change from the previous
value.

From the table, we can observe fluctuations in stock prices. For
example, on January 9, 2007, the price dropped by -1.06%, but on January
10, 2007, it increased by 1.43%. Similarly, in February 2007, the price
first increased, then declined again. These ups and downs indicate
short-term volatility in Boeing’s stock. The presence of negative values
suggests periods of decline, while positive values show recoveries.

# Visual Summaries

## Histogram: BA returns

    hist(ba.ret, breaks=100, main="BA's Cont. Comp. Returns", xlab="Returns")

![image](https://github.com/user-attachments/assets/a68a37cd-924f-41d1-9c95-93b2363de752)

The distribution is bell-shaped indicating a normal-like distribution.
Most returns are clustered near zero.

## Histogram for mondays returns

    hist(ba.ret[wday(index(ba.ret))==2], breaks=50, main="BA's Monday Cont. Comp. Returns", xlab="Returns")

![image](https://github.com/user-attachments/assets/f51d97c3-509f-4c47-a1ab-86bea5e624c3)

We can the same thing here as well. The distribution is bell-shaped
indicating a normal-like distribution. Most returns are clustered near
zero.

## Histogram for fridays returns

    hist(ba.ret[wday(index(ba.ret))==6], breaks=50, main="BA's Friday Cont. Comp. Returns", xlab="Returns")

![image](https://github.com/user-attachments/assets/1d76e246-2a6b-4c2e-b69a-b32a3dd82d00)

We can see its very similar in this histogram too. The only difference I
see is that this histogram has more observations on the negative side.
The distribution is bell-shaped indicating a normal-like distribution.
Most returns are clustered near zero.

## Empirical Cumulative Distribution of Fridays Return

    plot(ecdf(as.vector(ba.ret[wday(index(ba.ret))==6])), main="Friday ECDF")

![image](https://github.com/user-attachments/assets/e9390791-97c1-44f5-b88e-1020a001e170)

We see that most observations is in the range of -0.5 to 0.5 and close
to 0. This is matches with the histogram that we plotted before. We can
say it has a normal-like distribution and returns are stable.

## Comparison of Empirical Cumulative Distributions of Monday (red) and Fridays (black) Return

    plot(ecdf(as.vector(ba.ret[wday(index(ba.ret))==6])), main="ECDF Distributions")
    lines(ecdf(as.vector(ba.ret[wday(index(ba.ret))==2])), col="red")

![image](https://github.com/user-attachments/assets/56d562ef-c498-4a54-8fbb-8c3dc1acbf5f)

We can see that Monday and Friday returns are almost same. Most
observations is in the range of -0.5 to 0.5 and close to 0. We can say
it has a normal-like distribution and returns are stable.

# Mean Returns

## Mean of the weekday returns

    # What about mean returns of weekdays..
    mean.ret <- cbind(
    mean(ba.ret[wday(index(ba.ret))==2], na.rm=T),
    mean(ba.ret[wday(index(ba.ret))==3], na.rm=T),
    mean(ba.ret[wday(index(ba.ret))==4], na.rm=T),
    mean(ba.ret[wday(index(ba.ret))==5], na.rm=T),
    mean(ba.ret[wday(index(ba.ret))==6], na.rm=T))
    colnames(mean.ret) <- levels(wday(index(ba.ret), label=T))[2:6]
    rownames(mean.ret) <- "Mean Returns"

    # Lets see up to 6 digits..
    round(mean.ret, 6)

    ##                   Pzt     Sal      Çar      Per      Cum
    ## Mean Returns 0.000257 0.00016 0.000353 0.000311 0.000155

Among these values, Thursday stands out with the highest mean return
(`0.000247`), while Friday shows the lowest return (`0.000112`). This
pattern might indicate that Thursday is generally a more profitable day
for investments, while Friday could be associated with lower
performance.

# BA Monday Prices Line Chart

    plot(ba[wday(index(ba))==2], main="BA Mondays Prices", ylab="$")

![image](https://github.com/user-attachments/assets/16ee083e-ca64-4e1b-8c73-dd8bfcf4567a)


    # zoo type..
    plot(as.zoo(ba[wday(index(ba))==2]), main="BA Mondays Prices", ylab="$", xlab="Date")

![image](https://github.com/user-attachments/assets/a9f30acd-7859-49f8-bbe5-2607467a2605)

We see that before the 2017 it is increasing in its normal trend. Before
2017 its around 100 dollars. After 2017 prices increase exponentially
and rises up to 400 dollars. After 2020 prices declines significantly.
After 2021 it is increases around 200 dollars.

# Monthly Series

    # Convert to monthly series
    ba.m <- Ad(to.monthly(BA))
    # Get the return series similar to above
    ba.mret <- diff(log(ba.m))
    # The mean of all montly returns.. (up to 6 digits)
    round(mean(ba.mret, na.rm=T), 6)

    ## [1] 0.005184

    # What about the yearly mean returns calculated from monthly returns.. (up to 6 digits).. Seems better than T-Bonds.. Remember utility functions..
    round((1+mean(ba.mret, na.rm=T))^12-1, 6)

    ## [1] 0.064013

    # Here is the mean yearly return calculated from data
    round(mean(diff(log(Ad(to.yearly(BA)))), na.rm=T), 6)

    ## [1] 0.063869

    # Get some mean return value fo specific months.. 
    head(ba.mret[month(index(ba.mret))==1], na.rm=T)

    ##           BA.Adjusted
    ## Oca 2007           NA
    ## Oca 2008 -0.050174226
    ## Oca 2009 -0.008471988
    ## Oca 2010  0.112906136
    ## Oca 2011  0.062659579
    ## Oca 2012  0.011252376

In January 2007, there is no available data, but from January 2008, we
see a negative value (`-0.050174852`), indicating a decline compared to
the previous period. The following year (January 2009) also shows a
negative value (`-0.008472528`), but the decline is much smaller,
suggesting a possible recovery or stabilization.

A strong positive increase is observed in January 2010 (`0.112906588`),
marking a significant improvement. However, the subsequent years show
lower, yet still positive returns: January 2011 (`0.062659720`) and
January 2012 (`0.011252313`). This indicates a general upward trend,
though the growth rate seems to be slowing over time.

    # Mean January Returns.. (check your R and OS language for different month labels..)
    mean(ba.mret[month(index(ba.mret))==1], na.rm=T)

    ## [1] 0.007311456

    # February..
    mean(ba.mret[month(index(ba.mret))==2], na.rm=T)

    ## [1] 0.00295061

# BA Monthly Returns Bar Plot (2017 - 2025)

    # All January returns since 2007
    barplot(ba.mret[month(index(ba.mret))==1])

![image](https://github.com/user-attachments/assets/bbb4a7b4-2997-41b7-84b8-ebc90dd9612b)

When we look at this bar plot we can see that there are peaks in 2016
and 2019 indicate growth, while troughs around 2016 and 2022 highlight
declines, showing variability over time.

# Statistical Tests

## Kolmogorov-Smirnov Test

    # Compare Mondays and Tuesdays..
    ks.test(ba.ret[wday(index(ba.ret))==2], ba.ret[wday(index(ba.ret))==3])

    ## 
    ##  Asymptotic two-sample Kolmogorov-Smirnov test
    ## 
    ## data:  ba.ret[wday(index(ba.ret)) == 2] and ba.ret[wday(index(ba.ret)) == 3]
    ## D = 0.067427, p-value = 0.03243
    ## alternative hypothesis: two-sided

The test statistic (`D = 0.063855`) represents the maximum difference
between the two cumulative distributions. The p-value of (`0.05105`) is
close to (`0.05`), suggesting that there is weak evidence against the
null hypothesis, but it does not reach conventional significance levels.
Therefore, the difference in return distributions between these two days
is not statistically significant at the 5% level, although it is
marginal.

    # Compare Mondays and Fridays..
    ks.test(ba.ret[wday(index(ba.ret))==2], ba.ret[wday(index(ba.ret))==6])

    ## 
    ##  Asymptotic two-sample Kolmogorov-Smirnov test
    ## 
    ## data:  ba.ret[wday(index(ba.ret)) == 2] and ba.ret[wday(index(ba.ret)) == 6]
    ## D = 0.049227, p-value = 0.2275
    ## alternative hypothesis: two-sided

The test statistic (`D = 0.049352`) indicates the maximum difference
between their cumulative distributions. The p-value of (`0.2286`) is
relatively high, suggesting no significant evidence to reject the null
hypothesis. This means the return distributions of Monday and Friday are
statistically similar, and there is no strong indication of a meaningful
difference between them. \## p-value Matrix

    # Let's obtain all.. Create 5*5 matrix.. We use only upper-triangle
    # See the structure of ks.test result first..
    p.matr <- matrix(rep(0, 5*5), nrow=5)
    colnames(p.matr) <- rownames(p.matr) <- levels(wday(index(ba.ret), label=T))[2:6]

    for (i in 2:6){
      for (j in i:6){
        p.matr[i-1,j-1] <- ks.test(as.numeric(ba.ret[wday(index(ba.ret))==i]), as.numeric(ba.ret[wday(index(ba.ret))==j]))$p.value
      }
    }

    # p-vales matrix of  Kolmogorov-Smirnov Tests
    round(p.matr, 3)

    ##     Pzt   Sal   Çar   Per   Cum
    ## Pzt   1 0.993 0.674 0.060 0.787
    ## Sal   0 1.000 0.844 0.098 0.729
    ## Çar   0 0.000 1.000 0.087 0.650
    ## Per   0 0.000 0.000 1.000 0.080
    ## Cum   0 0.000 0.000 0.000 1.000

Monday and Tuesday have a strong correlation (`0.997`), meaning their
return patterns are quite similar. In contrast, Thursday has a weak
relationship with earlier weekdays, especially Monday (`0.057`) and
Tuesday (\`0.107), suggesting a different return behavior. Friday is
completely uncorrelated with Monday through Wednesday, indicating a
distinct return distribution.

    # Let's obtain all months returns.. Create 12*12 matrix.. We use only upper-triangle
    # See the structure of ks.test result first..
    pm.matr <- matrix(rep(0, 12*12), nrow=12)
    colnames(pm.matr) <- rownames(pm.matr) <- levels(month(index(ba.mret), label=T))

    for (i in 1:12){
      for (j in i:12){
        pm.matr[i,j] <- ks.test(as.numeric(ba.mret[month(index(ba.mret))==i]), as.numeric(ba.mret[month(index(ba.mret))==j]))$p.value
      }
    }

    # p-vales matrix of  Kolmogorov-Smirnov Tests
    round(pm.matr, 3)

    ##     Oca   Şub   Mar   Nis   May   Haz   Tem   Ağu   Eyl   Eki   Kas   Ara
    ## Oca   1 0.623 0.966 0.808 0.654 0.781 0.972 0.503 0.781 0.972 0.503 0.503
    ## Şub   0 1.000 0.808 0.978 0.538 0.587 0.882 0.181 0.870 0.338 0.087 0.960
    ## Mar   0 0.000 1.000 0.808 0.978 0.703 0.792 0.825 0.808 0.999 0.159 0.273
    ## Nis   0 0.000 0.000 1.000 1.000 0.758 0.993 0.289 0.893 0.528 0.567 0.960
    ## May   0 0.000 0.000 0.000 1.000 0.470 0.911 0.338 0.664 0.567 0.587 0.758
    ## Haz   0 0.000 0.000 0.000 0.000 1.000 0.781 0.781 0.781 0.781 0.132 0.503
    ## Tem   0 0.000 0.000 0.000 0.000 0.000 1.000 0.275 0.781 0.781 0.781 0.972
    ## Ağu   0 0.000 0.000 0.000 0.000 0.000 0.000 1.000 0.503 0.972 0.132 0.132
    ## Eyl   0 0.000 0.000 0.000 0.000 0.000 0.000 0.000 1.000 0.972 0.503 0.781
    ## Eki   0 0.000 0.000 0.000 0.000 0.000 0.000 0.000 0.000 1.000 0.275 0.275
    ## Kas   0 0.000 0.000 0.000 0.000 0.000 0.000 0.000 0.000 0.000 1.000 0.275
    ## Ara   0 0.000 0.000 0.000 0.000 0.000 0.000 0.000 0.000 0.000 0.000 1.000

January, March, and July show strong correlations, suggesting similar
return behaviors during these months. February and April also have a
high correlation, meaning their return patterns are quite similar. In
contrast, August and November display weaker relationships with other
months, indicating unique return trends. June and September maintain
moderate correlations across multiple months, reflecting some
consistency while still showing variations. These results suggest that
stock returns may follow seasonal trends, where certain months share
similar performance characteristics while others differ significantly.

## Time Series Decomposition

    ba.monthly.adj <- Ad(to.monthly(BA))

    ba.ts <- ts(as.numeric(ba.monthly.adj), start = c(2007, 1), frequency = 12)

    ba.stl <- stl(ba.ts, s.window = "periodic")

    plot(ba.stl)

![image](https://github.com/user-attachments/assets/b530ca63-f531-4a74-9360-e3b2d5e6aa40)

The graph presents a time series decomposition, breaking the data into
four components: observed data, seasonal pattern, trend, and remainder
(residuals). The seasonal component shows a repeating pattern,
indicating periodic fluctuations. The trend captures long-term
movements, with a steady rise until 2019, followed by a decline. The
remainder represents irregular variations, with noticeable spikes around
2020. This analysis helps identify underlying patterns and anomalies in
the data.

## Forecasting

    library(forecast)
    library(ggplot2)

    ba.ets <- ets(ba.ts)
    autoplot(forecast(ba.ets, h = 12)) +
      ggtitle("BA Monthly Adjusted Price Forecast")

![image](https://github.com/user-attachments/assets/6fde2905-23a5-4700-839f-ed117ed88ff9)


    summary(ba.ets)

    ## ETS(M,N,N) 
    ## 
    ## Call:
    ## ets(y = ba.ts)
    ## 
    ##   Smoothing parameters:
    ##     alpha = 0.9999 
    ## 
    ##   Initial states:
    ##     l = 64.0943 
    ## 
    ##   sigma:  0.0991
    ## 
    ##      AIC     AICc      BIC 
    ## 2283.843 2283.953 2294.037 
    ## 
    ## Training set error measures:
    ##                     ME     RMSE      MAE          MPE     MAPE     MASE
    ## Training set 0.6256925 18.63853 11.21241 -0.006690992 7.354645 0.249619
    ##                    ACF1
    ## Training set 0.02807861

The graph shows Boeing’s monthly adjusted stock price with a forecast
for the near future. The stock saw steady growth until 2019, followed by
a sharp decline in 2020 and fluctuating recovery afterward. The
blue-shaded forecast area indicates possible price movements, with
uncertainty increasing over time. The stock’s future trend remains
uncertain, depending on market and economic conditions.

# Smoothing

## Adjusted Close

    library(zoo)
    library(fpp3)
    library(mgcv)

    autoplot(ba) +
      geom_smooth(method = "loess", span = 0.3, color = "red") +
      labs(
        title = "Loess Smoothing: Adjusted Close Prices",
        x = "Date",
        y = "Adjusted Close ($)"
      ) +
      theme_minimal() +
      theme(
        panel.grid = element_blank(),
        axis.line = element_line(linewidth = 1, colour = "grey80"))

![image](https://github.com/user-attachments/assets/6af1fe33-383a-4b12-99b2-8472ad226506)

The black line represents the actual prices, while the red line
illustrates the smoothed trend using `Loess` smoothing. The smoothing
technique helps reveal the general pattern in stock price movements by
reducing short-term fluctuations. The graph shows a sharp rise in prices
around 2020, followed by a significant decline and continued variations.

## Volume

    autoplot(BA$BA.Volume) +
      geom_smooth(method = "loess", span = 0.3, color = "red") +
      labs(
        title = "Loess Smoothing: Volume",
        x = "Date",
        y = "Volume"
      ) +
      theme_minimal() +
      theme(
        panel.grid = element_blank(),
        axis.line = element_line(linewidth = 1, colour = "grey80"))

    ## `geom_smooth()` using formula = 'y ~ x'

![image](https://github.com/user-attachments/assets/3f56c721-1821-4a6e-bbd9-3d9f9440ed2c)

    autoplot(BA$BA.Volume) +
      geom_smooth(method = "gam", formula = y ~ s(x, bs = "cs"), color = "red") +
      labs(
        title = "GAM Smoothing: Volume",
        x = "Date",
        y = "Volume"
      ) +
      theme_minimal() +
      theme(
        panel.grid = element_blank(),
        axis.line = element_line(linewidth = 1, colour = "grey80"))

![image](https://github.com/user-attachments/assets/89b510fa-896a-4880-9893-5f0c59307d71)

When we look at both `LOESS` and `GAM` smoothing plots, we can see that
the `LOESS` captures more details and fluctuations in the data, while
`GAM` produces a slightly smoother trend.

## High Prices

    autoplot(BA$BA.High) +
      geom_smooth(method = "loess", span = 0.3, color = "red") +
      labs(
        title = "Loess Smoothing: High Prices",
        x = "Date",
        y = "High Price ($)"
      ) +
      theme_minimal() +
      theme(
        panel.grid = element_blank(),
        axis.line = element_line(linewidth = 1, colour = "grey80"))

    ## `geom_smooth()` using formula = 'y ~ x'

![image](https://github.com/user-attachments/assets/7c438f8b-77b8-4865-93ca-86d43f578766)

    autoplot(BA$BA.High) +
      geom_smooth(method = "lm", formula = y ~ poly(x, 3), color = "red") +
      labs(
        title = "Polynomial Regression Smoothing: High Prices",
        x = "Date",
        y = "High Price ($)"
      ) +
      theme_minimal() +
      theme(
        panel.grid = element_blank(),
        axis.line = element_line(linewidth = 1, colour = "grey80"))

![image](https://github.com/user-attachments/assets/488d253d-93b2-471c-b35e-b5b7a4cfbad6)

When we look at both `LOESS` and `Polynomial Regression` smoothing
plots, we can see that the `LOESS` captures more details and
fluctuations in the data, while `Polynomial Regression` produces a
smoother trend.

## Low Prices

    library(patchwork)

    plot1 <- autoplot(BA$BA.Low) +
      geom_smooth(method = "loess", span = 0.1, color = "red") +
      labs(
        title = "Loess Smoothing (span=0.1): Low Prices",
        x = "Date",
        y = "Low Price ($)"
      ) +
      theme_minimal() +
      theme(
        panel.grid = element_blank(),
        axis.line = element_line(linewidth = 1, colour = "grey80"))

    plot2 <- autoplot(BA$BA.Low) +
      geom_smooth(method = "loess", span = 0.3, color = "red") +
      labs(
        title = "Loess Smoothing (span=0.3): Low Prices",
        x = "Date",
        y = "Low Price ($)"
      ) +
      theme_minimal() +
      theme(
        panel.grid = element_blank(),
        axis.line = element_line(linewidth = 1, colour = "grey80"))

    plot3 <- autoplot(BA$BA.Low) +
      geom_smooth(method = "loess", span = 0.5, color = "red") +
      labs(
        title = "Loess Smoothing (span=0.5): Low Prices",
        x = "Date",
        y = "Low Price ($)"
      ) +
      theme_minimal() +
      theme(
        panel.grid = element_blank(),
        axis.line = element_line(linewidth = 1, colour = "grey80"))

    plot4 <- autoplot(BA$BA.Low) +
      geom_smooth(method = "loess", span = 0.7, color = "red") +
      labs(
        title = "Loess Smoothing (span=0.7): Low Prices",
        x = "Date",
        y = "Low Price ($)"
      ) +
      theme_minimal() +
      theme(
        panel.grid = element_blank(),
        axis.line = element_line(linewidth = 1, colour = "grey80"))

    (plot1 + plot2) / (plot3 + plot4)

![image](https://github.com/user-attachments/assets/9ebcee89-7403-465b-b686-45d2765e0828)

The black lines show the actual low prices, while the red lines
represent smoothed data. The graphs demonstrate how different spans of
Loess smoothing affect the interpretation of trends. A smaller span,
like (`0.1`), captures more details and fluctuations in the data, while
a larger span, such as (`0.7`), produces a smoother trend, making it
easier to observe the general direction of prices over time.

# Conclusion

The analysis of Boeing Company (`BA`) stock data from 2007 to 2025 has
revealed important trends and patterns in return distributions across
different timeframes. Weekly return comparisons demonstrated notable
variations, particularly with Thursday showing higher average returns,
while Friday exhibited lower performance, suggesting potential weekday
effects on market behavior. `Kolmogorov-Smirnov` tests indicated weak or
non-significant differences between return distributions for specific
days, reinforcing the idea that while some patterns exist, they may not
be statistically strong.

In the monthly analysis, correlation values highlighted seasonal
influences, with certain months sharing similar return distributions
while others diverged. January, March, and July displayed stronger
correlations, while August and November appeared to follow distinct
patterns, reflecting potential market seasonality. Additionally,
smoothing techniques, including `LOESS`, `Polynomial Regression`, and
`GAM`, helped reveal long-term trends, showing periods of growth,
volatility, and stabilization in BA’s stock performance.

**Note:** Some of the interpretations and explanations were refined with
the help of GPT.
