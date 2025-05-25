<h1>
Boeing Company Stock Price Series
</h1>

In this assignment I have done some time series analysis for Boeing
Company stock prices.

## Intstalling Libraries

    library(quantmod)
    library(xts)
    library(lubridate)

## Loading the Data

    load("djdata.RData")

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

## Looking for the first and last few observations of data

    head(BA)

    ##            BA.Open BA.High BA.Low BA.Close BA.Volume BA.Adjusted
    ## 2007-01-03   88.90   90.30  88.45    89.17   4871700    64.40574
    ## 2007-01-04   88.34   89.83  87.01    89.53   2718900    64.66573
    ## 2007-01-05   89.78   90.00  88.50    89.15   3285900    64.39128
    ## 2007-01-08   88.61   89.41  87.56    88.94   2989000    64.23959
    ## 2007-01-09   88.93   89.71  87.56    88.00   4193800    63.56064
    ## 2007-01-10   88.04   89.34  88.00    89.27   3955200    64.47795

    tail(BA)

    ##            BA.Open BA.High BA.Low BA.Close BA.Volume BA.Adjusted
    ## 2025-05-16  205.69  206.24 203.02   205.82   8496800      205.82
    ## 2025-05-19  203.00  205.60 202.30   205.25   5740200      205.25
    ## 2025-05-20  205.00  208.62 205.00   207.67   5876000      207.67
    ## 2025-05-21  206.60  207.12 202.43   203.21   6616300      203.21
    ## 2025-05-22  202.53  204.73 201.85   203.41   3634500      203.41
    ## 2025-05-23  199.95  203.20 198.75   202.36   5249600      202.36

## Plot for opening, closing prices, high and low values and the volume

    plot(as.zoo(BA))

![image](https://github.com/user-attachments/assets/c8fdd95f-a40d-4fe2-94eb-03da914e0848)

We see that the BA.Open, BA.High, BA.Low, and BA.Close graphs display
stock prices at different points, with clear volatility and a big drop
around 2020. The BA.Volume graph highlights trading activity, with
noticeable spikes that likely indicate significant events or decisions
made by investors. The BA.Adjusted graph shows the adjusted closing
prices, which take dividends and stock splits into account, giving a
more accurate picture of value.

## Line Chart (2007 - 2025)

    plot(BA[,-5])

![image](https://github.com/user-attachments/assets/8bf385ed-b5f2-4737-b4df-6358cc6d83e9)

When we look at this line graph we can see that it remains stable until
2016, followed by a sharp rise peaking in 2019. A sudden drop in 2020
that I assume its because of the pandemics. After 2021, the values
fluctuate but stabilize at a lower level than the peak.

## Financial Data

    # First few days without labelling.
    head(wday(index(BA), label=F))

    ## [1] 4 5 6 2 3 4

    # First few days with labelling..
    head(wday(index(BA), label=T))

    ## [1] Çar Per Cum Pzt Sal Çar
    ## Levels: Paz < Pzt < Sal < Çar < Per < Cum < Cmt

    # result is factor object..
    str(head(wday(index(BA), label=T)))

    ##  Ord.factor w/ 7 levels "Paz"<"Pzt"<"Sal"<..: 4 5 6 2 3 4

    is.factor(head(wday(index(BA), label=T)))

    ## [1] TRUE

    # Get the first few days as character (instead of factor)
    paste(head(wday(index(BA), label=T)))

    ## [1] "Çar" "Per" "Cum" "Pzt" "Sal" "Çar"

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
    #     paste(month(dx, label=T, abbr = F)), 
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

## Close, Adjusted Close, Day-of-week

    ba <- Ad(BA)

    # Get Mondays
    head(ba[wday(index(ba))==2])

    ##            BA.Adjusted
    ## 2007-01-08    64.23959
    ## 2007-01-22    61.82717
    ## 2007-01-29    61.75498
    ## 2007-02-05    65.52525
    ## 2007-02-12    64.67621
    ## 2007-02-26    64.48045

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
    ## 2007-01-08 -0.0023586146
    ## 2007-01-22 -0.0347853335
    ## 2007-01-29  0.0008194875
    ## 2007-02-05  0.0074123740
    ## 2007-02-12 -0.0089287408
    ## 2007-02-26 -0.0150666360

    # Data and return series together..
    head(merge(ba, ba.ret))

    ##            BA.Adjusted BA.Adjusted.1
    ## 2007-01-03    64.40574            NA
    ## 2007-01-04    64.66573   0.004028578
    ## 2007-01-05    64.39128  -0.004253082
    ## 2007-01-08    64.23959  -0.002358615
    ## 2007-01-09    63.56064  -0.010625177
    ## 2007-01-10    64.47795   0.014328875

    # Head of mondays returns with levels.
    head(merge(ba, ba.ret)[wday(merge(ba, ba.ret))==2])

    ##            BA.Adjusted BA.Adjusted.1
    ## 2007-01-08    64.23959 -0.0023586146
    ## 2007-01-22    61.82717 -0.0347853335
    ## 2007-01-29    61.75498  0.0008194875
    ## 2007-02-05    65.52525  0.0074123740
    ## 2007-02-12    64.67621 -0.0089287408
    ## 2007-02-26    64.48045 -0.0150666360

## Histogram: BA returns

    hist(ba.ret, breaks=100, main="BA's Cont. Comp. Returns", xlab="Returns")

![image](https://github.com/user-attachments/assets/791f7856-fe62-44a6-b34e-29e427fdb87e)

The distribution is bell-shaped indicating a normal-like distribution.
Most returns are clustered near zero.

## Histogram for mondays returns

    hist(ba.ret[wday(index(ba.ret))==2], breaks=50, main="BA's Monday Cont. Comp. Returns", xlab="Returns")

![image](https://github.com/user-attachments/assets/840a31b8-ceb8-4651-b5fb-0c8a9e3d318c)

We can the same thing here as well. The distribution is bell-shaped
indicating a normal-like distribution. Most returns are clustered near
zero.

## Histogram for fridays returns

    hist(ba.ret[wday(index(ba.ret))==6], breaks=50, main="BA's Friday Cont. Comp. Returns", xlab="Returns")

![image](https://github.com/user-attachments/assets/9eeff46d-d3d1-4a4c-a236-5d18e64d1678)

We can see its very similar in this histogram too. The only difference I
see is that this histogram has more observations on the negative side.
The distribution is bell-shaped indicating a normal-like distribution.
Most returns are clustered near zero.

## Empirical Cumulative Distribution of Fridays Return

    plot(ecdf(as.vector(ba.ret[wday(index(ba.ret))==6])), main="Friday ECDF")

![image](https://github.com/user-attachments/assets/122a8476-ea02-4922-8460-ef4e7f5a9556)

We see that most observations is in the range of -0.5 to 0.5 and close
to 0. This is matches with the histogram that we plotted before. We can
say it has a normal-like distribution and returns are stable.

## Comparison of Empirical Cumulative Distributions of Monday (red) and Fridays (black) Return

    plot(ecdf(as.vector(ba.ret[wday(index(ba.ret))==6])), main="ECDF Distributions")
    lines(ecdf(as.vector(ba.ret[wday(index(ba.ret))==2])), col="red")

![image](https://github.com/user-attachments/assets/ba9ea030-b7ac-4b4a-accd-ed8013cbdbfa)

We can see that Monday and Friday returns are almost same. Most
observations is in the range of -0.5 to 0.5 and close to 0. We can say
it has a normal-like distribution and returns are stable.

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

## BA Monday Prices Line Chart

    plot(ba[wday(index(ba))==2], main="BA Mondays Prices", ylab="$")

![image](https://github.com/user-attachments/assets/58401b10-3ab8-43e7-a155-9a43bfb4b8ae)

    # zoo type..
    plot(as.zoo(ba[wday(index(ba))==2]), main="BA Mondays Prices", ylab="$", xlab="Date")

![image](https://github.com/user-attachments/assets/80ded71d-a58d-4243-bf9e-a5eb1894f982)

We see that before the 2017 it is increasing in its normal trend. Before
2017 its around 100 dollars. After 2017 prices increase exponentially
and rises up to 400 dollars. After 2020 prices declines significantly.
After 2021 it is increases around 200 dollars.

## Monthly Series

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
    ## Oca 2008 -0.050174408
    ## Oca 2009 -0.008472587
    ## Oca 2010  0.112906650
    ## Oca 2011  0.062659647
    ## Oca 2012  0.011251869

    # Mean January Returns.. (check your R and OS language for different month labels..)
    mean(ba.mret[month(index(ba.mret))==1], na.rm=T)

    ## [1] 0.007311398

    # February..
    mean(ba.mret[month(index(ba.mret))==2], na.rm=T)

    ## [1] 0.002950705

## BA Monthly Returns Bar Plot (2017 - 2025)

    # All January returns since 2007
    barplot(ba.mret[month(index(ba.mret))==1])

![image](https://github.com/user-attachments/assets/c0793e82-acb9-4488-9744-d1f5ff4a41b4)

When we look at this bar plot we can see that there are peaks in 2016
and 2019 indicate growth, while troughs around 2016 and 2022 highlight
declines, showing variability over time.

## Comparing Return Distribution

    # Compare Mondays and Tuesdays..
    ks.test(ba.ret[wday(index(ba.ret))==2], ba.ret[wday(index(ba.ret))==3])

    ## 
    ##  Asymptotic two-sample Kolmogorov-Smirnov test
    ## 
    ## data:  ba.ret[wday(index(ba.ret)) == 2] and ba.ret[wday(index(ba.ret)) == 3]
    ## D = 0.067427, p-value = 0.03243
    ## alternative hypothesis: two-sided

    # Compare Mondays and Fridays..
    ks.test(ba.ret[wday(index(ba.ret))==2], ba.ret[wday(index(ba.ret))==6])

    ## 
    ##  Asymptotic two-sample Kolmogorov-Smirnov test
    ## 
    ## data:  ba.ret[wday(index(ba.ret)) == 2] and ba.ret[wday(index(ba.ret)) == 6]
    ## D = 0.049227, p-value = 0.2275
    ## alternative hypothesis: two-sided

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
    ## Pzt   1 0.993 0.674 0.060 0.806
    ## Sal   0 1.000 0.844 0.098 0.729
    ## Çar   0 0.000 1.000 0.087 0.650
    ## Per   0 0.000 0.000 1.000 0.080
    ## Cum   0 0.000 0.000 0.000 1.000

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
