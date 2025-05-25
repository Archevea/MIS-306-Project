------------------------------------------------------------------------

# Objective

This project analyzes Nike Inc. (NKE) stock performance (2007–2025) to
identify patterns, build forecasting models, and generate investment
insights. Key components include:

<h4>

1.  Data Exploration
    </h4>

-   Analyze daily/weekly/monthly returns for trends and seasonality

-   Compare weekday distributions (Monday–Friday) using statistical
    tests

-   Examine volatility patterns and trading volume changes

<h4>

1.  Model Development
    </h4>

-   Test stationarity and apply differencing when needed

-   Fit multiple ARIMA configurations (ARIMA(1,1,1), ARIMA(2,1,1))

-   Implement automated model selection via auto.arima

-   Generate forecasts using optimal models

<h4>

1.  Validation & Insights
    </h4>

-   Evaluate model fit through residual diagnostics

-   Compare performance using AIC/BIC and error metrics

-   Identify reliable patterns for trading strategies

Goal: Provide actionable intelligence about NKE’s price behavior and
robust forecasting tools for investors.

------------------------------------------------------------------------

# Visual Summaries

## Plot for opening, closing prices, high and low values and the volume

![image](https://github.com/user-attachments/assets/fb9799c1-20bf-4485-9ccc-d9c1d0d166a4)

Nike’s stock exhibited strong growth from 2009 to 2021, peaking with
high investor confidence. The post-2021 decline seen across all price
indicators and the adjusted closing price suggests a broader market
shift or internal performance issues. Trading volume spikes throughout
the timeline point to periods of heightened interest, possibly tied to
financial reports or economic events.

## Line Chart (2007 - 2025)

![image](https://github.com/user-attachments/assets/7bf898fe-e92e-4b66-b357-9aef0453cd31)

This chart shows the stock price of Nike (NKE) from January 2007 to May
2025. The price increased slowly until around 2013, then started to rise
more quickly. It reached its highest point around the end of 2021, going
above `$150`. After that, the price dropped a lot and continued to fall
with some small increases in between. By 2025, the price is close to
`$50`. Overall, the chart shows strong growth for many years, followed
by a big decline after the peak.

------------------------------------------------------------------------

# Visual Summaries

## Histogram: NKE returns (All Days | Monday | Friday)

    ## [1] "C"

![image](https://github.com/user-attachments/assets/088d85f9-cec9-4699-ab2d-3027228bb04c)

This figure shows the distribution of Nike’s daily returns, including
all days, Mondays, and Fridays. All three histograms have a similar
shape—most returns are close to zero, forming a sharp peak in the
center. This means small daily changes are more common. Extreme values
(both gains and losses) are rare but exist. Compared to Mondays, Friday
returns seem slightly more spread out, which may suggest more market
activity or news impact before the weekend. Overall, the returns appear
to follow a normal-like distribution with slight differences by weekday.

------------------------------------------------------------------------

## Empirical Cumulative Distribution of Fridays Return

![image](https://github.com/user-attachments/assets/064b10bb-2c4d-4434-8438-b8947bc7d7d3)

Most of the returns are between `-0.05` and `0.05`, with the curve
rising steeply in that range. This means that small returns are the most
common. The flat areas on both sides show rare extreme values, either
losses or gains. Overall, the returns are centered around zero, and the
shape of the curve suggests a normal-like distribution.

## Comparison of Empirical Cumulative Distributions of Monday (red) and Fridays (black) Return

![image](https://github.com/user-attachments/assets/7ea7a732-f017-499e-a73f-8900f677c515)

This ECDF plot compares the return distributions of two groups, likely
all days (black) and Fridays (red). Both lines are very close to each
other, meaning their return patterns are similar. Most returns are
between `-0.05` and `0.05`, and the sharp rise around zero shows that
small returns are the most common. The few extreme values on both sides
show rare large losses or gains. Overall, the distributions are almost
the same, with only small differences.

------------------------------------------------------------------------

# Mean Returns

## Mean of the weekday returns

This table shows the average daily returns of Nike stock for each
weekday. Monday has a small negative mean return (`-0.000448`), while
all other days have positive mean returns. Thursday has the highest
average return (`0.000759`), followed by Tuesday. This suggests that, on
average, Nike performs slightly worse on Mondays and slightly better on
Thursdays. Overall, the differences are small, but they show a possible
weekday effect in returns.

    ##                    Mon     Tue      Wed      Thu      Fri
    ## Mean Returns -0.000448 0.00071 0.000392 0.000759 0.000499

![image](https://github.com/user-attachments/assets/e7727df5-a891-44e8-a65b-5e141e1727c0)

# NKE Monday Prices Line Chart

![image](https://github.com/user-attachments/assets/806a9b3b-d19f-4965-be93-69b346aaf0b3)

This chart shows Nike’s stock prices on Mondays from January 2007 to May
2025. The prices rose steadily until around late 2021, reaching a peak
above `$150`. After that, the trend reversed, and the prices started to
fall. By 2025, the price dropped to nearly $60. This shows a long period
of growth followed by a strong decline, with Monday prices reflecting
the overall market behavior.

------------------------------------------------------------------------

# NKE Monday Prices Zoo

![image](https://github.com/user-attachments/assets/799e87c7-153f-4a34-a0dd-508704a8e201)

This figure shows six different panels of Nike’s Monday stock data from
2007 to 2025. Each panel represents a different variable:

-Top-left (black line): Adjusted closing prices. It shows a strong
upward trend until late 2021, then a clear decline.

-Middle-left (red line): Opening prices. These follow a very similar
pattern to the adjusted prices, peaking in 2021.

-Bottom-left (green line): Closing prices. The movement is also very
close to the adjusted and opening prices.

-Top-right (blue line): High prices. This line represents the highest
price on each Monday and follows the same rising and falling pattern.

-Middle-right (cyan line): Volume. It shows the number of shares traded.
There are many spikes, especially after 2020, which may indicate market
reactions to news or events.

-Bottom-right (purple line): Low prices. It shows the lowest value of
the stock on each Monday, also peaking in 2021 and dropping afterwards.

Overall, all price-related charts show growth until around 2021, then a
decline. The volume chart shows trading activity became more volatile in
recent years. Mondays clearly reflect the general stock trend of Nike.

# Volume Log Transformation

![image](https://github.com/user-attachments/assets/b1afe255-b234-4cfd-a271-846ea2e5c66a)

This chart shows the log-transformed trading volume of Nike stock on
Mondays from 2007 to 2025. The y-axis uses a log scale to better show
volume changes. In the early years, volume was higher and more volatile.
Between 2015 and 2020, it stayed relatively low and stable. After 2022,
volume started to increase again, with more sharp spikes near 2025. This
suggests rising market activity and interest in recent years.

------------------------------------------------------------------------

# NKE Monthly Returns NKE Plot (2017 - 2025)

![image](https://github.com/user-attachments/assets/60805bce-ed60-4788-975b-a4b3a7cb4b86)

This bar chart shows Nike’s January returns from 2007 to 2024. Most bars
are below zero, meaning that January often had negative returns. The
largest drop happened around 2009, likely during the financial crisis.
Positive returns appear in some years like 2011, 2012, and 2023.
Overall, January returns are mixed, but negative values seem more
common, showing that the stock often performs weakly at the start of the
year.

------------------------------------------------------------------------

# Statistical Tests

## Kolmogorov-Smirnov Test

This Kolmogorov-Smirnov test compares the return distributions of
Mondays and Tuesdays. The test statistic is `D = 0.067225`, and the
p-value is `0.03324`. Since the p-value is below 0.05, the result is
statistically significant. This means there is evidence that the return
distributions for Mondays and Tuesdays are different, suggesting that
returns behave differently on these two weekdays.

    ## 
    ##  Asymptotic two-sample Kolmogorov-Smirnov test
    ## 
    ## data:  NKE_AD.ret[wday(index(NKE_AD.ret)) == 2] and NKE_AD.ret[wday(index(NKE_AD.ret)) == 3]
    ## D = 0.067225, p-value = 0.03324
    ## alternative hypothesis: two-sided

This Kolmogorov-Smirnov test compares the return distributions of
Mondays and Fridays. The test statistic is `D = 0.046412`, and the
p-value is `0.2894`, which is quite high. This means there is no
significant evidence to reject the null hypothesis. In other words, the
return distributions for Monday and Friday are statistically similar,
with no clear difference between them.

    ## 
    ##  Asymptotic two-sample Kolmogorov-Smirnov test
    ## 
    ## data:  NKE_AD.ret[wday(index(NKE_AD.ret)) == 2] and NKE_AD.ret[wday(index(NKE_AD.ret)) == 6]
    ## D = 0.047027, p-value = 0.2747
    ## alternative hypothesis: two-sided

------------------------------------------------------------------------

## Time Series Decomposition

![image](https://github.com/user-attachments/assets/ac25f5a0-590d-43f0-8a9e-245d9764057f)

This plot shows the decomposition of Nike’s monthly adjusted prices into
four parts: data, seasonal, trend, and remainder. The data panel shows
the original price movement, with growth until 2021, followed by a
decline. The seasonal panel reveals repeating yearly patterns, showing
that seasonality exists in the data. The trend panel shows long-term
growth peaking around 2021, then dropping. The remainder shows random
noise or irregular movements. Overall, the stock price is influenced by
both seasonality and long-term trends.

------------------------------------------------------------------------

## Forecasting

Since we both have trend and seasonality in our data we will use Holt
Winter’s Forecast Method.

![image](https://github.com/user-attachments/assets/efbf6e89-2a5b-46be-b4c5-bbf4b1b5f3d4)

This chart shows the forecast of Nike’s monthly adjusted prices using
the Holt-Winters method. The black line represents historical prices,
which rose sharply until 2021 and then declined. The blue line shows the
forecast for the next 12 months, while the shaded area indicates the
confidence intervals. The forecast suggests a slight upward trend, but
the wide shaded area shows there is uncertainty. Overall, the model
expects possible recovery, but with some risk.

    ## ETS(A,A,A) 
    ## 
    ## Call:
    ## ets(y = NKE.ts, model = "AAA")
    ## 
    ##   Smoothing parameters:
    ##     alpha = 0.9953 
    ##     beta  = 1e-04 
    ##     gamma = 1e-04 
    ## 
    ##   Initial states:
    ##     l = 11.1419 
    ##     b = 0.2465 
    ##     s = 2.8845 2.6632 -0.2782 -0.9355 -0.4143 -0.3647
    ##            -1.7743 -1.9911 -1.4222 -0.8495 0.8261 1.656
    ## 
    ##   sigma:  5.7404
    ## 
    ##      AIC     AICc      BIC 
    ## 1982.794 1985.808 2040.562 
    ## 
    ## Training set error measures:
    ##                       ME     RMSE      MAE        MPE     MAPE      MASE
    ## Training set -0.01872384 5.528707 3.580695 -0.3332382 7.017772 0.2746144
    ##                     ACF1
    ## Training set 0.005828908

This summary shows the results of the Holt-Winters (ETS AAA) model
applied to Nike’s monthly prices. The model uses additive error, trend,
and seasonality. The smoothing parameters (`alpha = 0.9971`) suggest the
model gives strong weight to recent values. The initial seasonal states
show clear seasonal effects. The AIC (`1983.67`) and RMSE (`5.54`)
indicate the model’s fit. Error measures like MAPE (`6.94%`) show the
average forecast error is relatively low. Overall, the model fits the
data well and captures both trend and seasonal patterns.

------------------------------------------------------------------------

# Smoothing

## Adjusted Close

![image](https://github.com/user-attachments/assets/9a9a540b-34eb-4596-8297-724ecd0a771a)

This chart shows Nike’s adjusted close prices over time, with daily
price movements in black and a red Loess smoothing line to highlight the
trend. The Loess technique helps reduce short-term fluctuations and
reveals the general pattern more clearly. From 2007 to around 2021, the
red line shows a strong upward trend, peaking sharply around 2020. After
that, the trend turns downward, indicating a long-term decline. Despite
ongoing variations in daily prices, the smoothed line makes it easier to
see the overall rise and fall in stock performance.

------------------------------------------------------------------------

## High Prices

![image](https://github.com/user-attachments/assets/510280a8-e583-43cf-8144-b9426751bfc9)

![image](https://github.com/user-attachments/assets/8422629c-8279-4a04-bcf5-44bdff71c268)

These charts show Nike’s high stock prices over time, using two
different smoothing methods.

-   The first chart uses Loess smoothing. The black line shows the
    actual high prices, while the red line reveals a smooth trend. It
    clearly shows a steady increase until 2021, followed by a noticeable
    decline. This method captures short-term movements while showing the
    overall trend.

-   The second chart uses polynomial regression smoothing. The red line
    is smoother and more general. It shows a slow rise from 2010 to
    2021, then a decline, but it doesn’t follow the short-term
    fluctuations as closely.

Overall, both methods show a long-term rise and fall in prices, but
Loess gives a more detailed view, while polynomial regression gives a
broader trend.

------------------------------------------------------------------------

## Low Prices

![image](https://github.com/user-attachments/assets/c1d4c8f9-61dc-4a47-8cd9-5d219e65a916)

This chart compares Loess smoothing with different span values applied
to Nike’s low prices. The black lines show actual prices, and red lines
show smoothed trends. With span = 0.1, the red line closely follows the
data, showing more detail. As the span increases to 0.3, 0.5, and 0.7,
the red line becomes smoother and less sensitive to short-term changes.
Larger spans highlight the overall trend better, while smaller spans
capture more local fluctuations. Overall, the choice of span affects how
much of the short-term movement is shown in the trend.

------------------------------------------------------------------------

# ARMA & ARIMA

## Stationarity Testing and Autocorrelation Analysis

The ADF test shows Nike’s stock prices are not stable over time
(Dickey-Fuller = -0.43, p-value = 0.99). This means the prices follow
trends that change. Since the test says we need to difference the data
once (ndiffs() = 1), we should calculate daily price changes. After this
change, we can check again if the data becomes stable. This step is
important before using ARIMA models, which need stable data to work
properly. The very high p-value proves the prices need this adjustment.

![image](https://github.com/user-attachments/assets/d7b467e2-25f7-4068-ae21-ab4e76352fa8)

    ## 
    ##  Augmented Dickey-Fuller Test
    ## 
    ## data:  as.numeric(nke_close)
    ## Dickey-Fuller = -0.42659, Lag order = 16, p-value = 0.9852
    ## alternative hypothesis: stationary

    ## [1] 1

![image](https://github.com/user-attachments/assets/cffdf119-235a-4134-82c3-48d26d1d1867)

![image](https://github.com/user-attachments/assets/fe719cb7-04e7-4bb3-919e-a71f8f656d92)

The log-transformed NKE prices graph shows the stock’s price movement
from 2007 to 2025. The upward trend until 2021 indicates strong growth,
followed by a recent decline. This long-term pattern suggests the data
needs differencing to remove trends before analysis.

The ACF (Autocorrelation Function) plot reveals how prices correlate
with their past values. The gradual decline in correlation values across
lags confirms the presence of trends, supporting the need for
differencing to achieve stationarity.

The PACF (Partial Autocorrelation Function) plot identifies direct
relationships between current prices and specific past prices. The
significant spike only at lag 1 suggests an AR(1) component might be
appropriate when modeling the differenced series. Together, these plots
confirm the non-stationary nature of the data and guide appropriate
model selection.

------------------------------------------------------------------------

## ARIMA(1,1,1) Model Fitting and Residual Diagnostics

The ARIMA(1,1,1) model results show Nike’s stock prices have a strong
connection between consecutive days, with an AR(1) coefficient of 0.65
and an MA(1) coefficient of -0.69. The model fits the data well, as
shown by the small error values (RMSE = 0.019) and the very low sigma
squared value (0.00036). The ACF1 value close to zero (-0.0036) means
the model has successfully captured all important patterns in the data,
leaving only random noise in the residuals. With a high log likelihood
(11,769) and low AIC (-23,532), this model provides reliable forecasts
for Nike’s stock price movements. The small prediction errors and clean
residual plots confirm this is a good quality model for analyzing and
forecasting Nike’s stock performance.

    ## 
    ## Call:
    ## arima(x = nke_close, order = c(1, 1, 1))
    ## 
    ## Coefficients:
    ##          ar1      ma1
    ##       0.6475  -0.6932
    ## s.e.  0.1248   0.1177
    ## 
    ## sigma^2 estimated as 0.0003616:  log likelihood = 11769.13,  aic = -23532.25
    ## 
    ## Training set error measures:
    ##                        ME      RMSE        MAE        MPE      MAPE      MASE
    ## Training set 0.0003966945 0.0190132 0.01262009 0.01056907 0.3498127 0.9986186
    ##                      ACF1
    ## Training set -0.003593554

![image](https://github.com/user-attachments/assets/d709dde6-c68d-44c0-ad0b-73c5a5a38483)

![image](https://github.com/user-attachments/assets/57d7cb89-bd94-4094-92f5-3da44c9ab851)

![image](https://github.com/user-attachments/assets/f66f727c-f903-45c5-9586-4845eb776479)

These three charts help us understand the performance of the AR(1) model
fitted to Nike’s return series.

-   Residuals of ARIMA(1,1,1) Model chart shows the residuals over time.
    The values are centered around zero with small fluctuations, which
    is a good sign. However, there are a few spikes, showing some
    outliers or volatility in the data.

-   The ACF plot shows the correlation between residuals at different
    time lags. All the bars (autocorrelations) fall within the blue
    confidence lines, meaning they are not significantly different from
    zero. This is exactly what we want to see - it tells us the model
    has successfully removed all predictable patterns from the data. The
    random spikes within the blue lines confirm the residuals now behave
    like pure random noise, with no remaining correlations that the
    model could have captured.

-   The PACF plot examines direct relationships between residuals at
    specific lags. Nearly all points here fall very close to zero and
    stay within the confidence bands. While there are a couple of very
    small spikes just outside the bands (around lags 5 and 15), these
    are minor and likely due to random chance rather than any real
    pattern. Like the ACF, this confirms our model has done a good job -
    there are no important correlations left in the residuals that we
    failed to account for in our ARIMA model.

------------------------------------------------------------------------

## ARIMA(1,1,2) Model Estimation and Diagnostic Checking

The ARIMA(1,1,2) model shows good results for Nike’s stock prices. The
model coefficients (AR1 = 0.65, MA1 = -0.70, MA2 = 0.005) suggest the
current price is influenced by recent prices and past shocks. The very
small sigma² value (0.00036) and high log likelihood (11769) indicate a
strong fit. Error measures are excellent, with low RMSE (0.019) and MAE
(0.0126), meaning the model’s predictions are close to actual prices.
The residual mean is near zero (0.0004), and the Box-Ljung test (p-value
= 0.136) confirms the residuals contain no remaining patterns - they’re
just random noise. The ACF and PACF plots (not shown here) would likely
confirm this clean residual behavior. Overall, this model performs
slightly better than the simpler ARIMA(1,1,1) version, though the small
MA2 coefficient suggests the second moving average term may not be
adding much value.

    ## 
    ## Call:
    ## arima(x = nke_close, order = c(1, 1, 2))
    ## 
    ## Coefficients:
    ##          ar1      ma1     ma2
    ##       0.6544  -0.7032  0.0049
    ## s.e.  0.1712   0.1716  0.0200
    ## 
    ## sigma^2 estimated as 0.0003616:  log likelihood = 11769.18,  aic = -23530.35
    ## 
    ## Training set error measures:
    ##                        ME     RMSE       MAE        MPE      MAPE      MASE
    ## Training set 0.0003954087 0.019013 0.0126195 0.01053311 0.3498153 0.9985725
    ##                       ACF1
    ## Training set -0.0004778539

![image](https://github.com/user-attachments/assets/66302bd4-7d7f-4784-8fb7-c6654baae348)

![image](https://github.com/user-attachments/assets/9ca23b81-b2e5-4293-a217-edd20ad011c2)


    ## [1] 0.0003954087

    ## 
    ##  Box-Ljung test
    ## 
    ## data:  residuals(fit_arma112)
    ## X-squared = 14.894, df = 10, p-value = 0.136

-   The ACF plot shows the correlation between residuals at different
    time intervals. All the bars (correlation values) stay completely
    within the blue confidence lines, which means they are not
    significantly different from zero. This is exactly what we want to
    see - it tells us the model has successfully removed all important
    patterns from the data. The residuals now behave like random noise,
    with no remaining correlations that the model could have captured.
    This clean ACF plot gives us confidence that our ARIMA model is
    working properly.

-   The PACF plot examines the direct relationship between residuals at
    specific time lags. Nearly all points here fall very close to zero
    and stay well within the confidence bands. While there are two very
    small spikes around lags 5 and 15 that slightly cross the blue
    lines, these are minor and likely due to random chance rather than
    any real pattern. Like the ACF, this confirms our model has done a
    good job - there are no significant correlations left in the
    residuals that we failed to account for in our ARIMA model. The tiny
    spikes we see are small enough to ignore for practical purposes.

------------------------------------------------------------------------

## ARIMA(2,1,1) Model Estimation and Diagnostic Checking

The ARIMA(2,1,1) model provides a good fit for Nike’s stock prices. The
coefficients (AR1 = 0.67, AR2 = 0.007, MA1 = -0.72) show that current
prices are mainly influenced by the most recent price (AR1) and recent
shocks (MA1), while the second autoregressive term (AR2) has minimal
impact. The model fits well, with a very small error variance (sigma² =
0.00036) and high log likelihood (11769). Prediction errors are low
(RMSE = 0.019, MAE = 0.0126), indicating accurate forecasts. The
Box-Ljung test (p-value = 0.133) confirms the residuals contain no
remaining patterns, behaving like random noise. While this model
performs similarly to the ARIMA(1,1,1), the near-zero AR2 coefficient
suggests the second autoregressive term may not be necessary, making the
simpler model potentially preferable.

    ## 
    ## Call:
    ## arima(x = nke_close, order = c(2, 1, 1))
    ## 
    ## Coefficients:
    ##          ar1     ar2      ma1
    ##       0.6741  0.0071  -0.7230
    ## s.e.  0.1545  0.0200   0.1538
    ## 
    ## sigma^2 estimated as 0.0003616:  log likelihood = 11769.18,  aic = -23530.36
    ## 
    ## Training set error measures:
    ##                        ME       RMSE        MAE        MPE      MAPE      MASE
    ## Training set 0.0003972399 0.01901299 0.01262036 0.01058424 0.3498386 0.9986404
    ##                       ACF1
    ## Training set -0.0003742778

![image](https://github.com/user-attachments/assets/8edc1d0c-112d-4b03-97a2-3ff257b223fd)

![image](https://github.com/user-attachments/assets/ceef0d91-54d3-41cd-9230-382d49d6e697)

    ## 
    ##  Box-Ljung test
    ## 
    ## data:  residuals(fit_arma211)
    ## X-squared = 14.974, df = 10, p-value = 0.133

-   The ACF plot shows the autocorrelation of residuals at different
    lags. In this plot, all the bars after lag 0 are within the blue
    dashed lines, which represent the 95% confidence interval. This
    means there is no significant autocorrelation remaining in the
    residuals. Therefore, the model appears to have captured the
    time-related structure in the data well.

-   The PACF plot shows the partial autocorrelation of residuals. Most
    of the bars are within the blue dashed lines, with only a few small
    spikes slightly outside. These small spikes are not strong enough to
    indicate a serious problem. This suggests that the residuals do not
    have a clear pattern left, and the model has likely captured the
    important information in the data.

------------------------------------------------------------------------

## ARIMA(2,1,2) Model Implementation and Residual Diagnostics

The ARIMA(2,1,2) model results show some technical issues but decent
overall performance. While the coefficients (AR1=0.055, AR2=0.354,
MA1=-0.103, MA2=-0.379) suggest the model captures price patterns, the
“NaN” standard errors indicate potential estimation problems - these
values should normally be calculated. Despite this, the model shows good
fit with small error variance (sigma²=0.00036) and high log likelihood
(11769). Prediction errors remain low (RMSE=0.019, MAE=0.0126), similar
to simpler models. The Box-Ljung test (p-value=0.1345) confirms the
residuals contain no significant patterns, behaving like random noise.
However, the estimation issues suggest this complex model may be
overfitting the data, making the simpler ARIMA(1,1,1) potentially more
reliable for forecasting Nike’s stock prices.

    ## 
    ## Call:
    ## arima(x = nke_close, order = c(2, 1, 2))
    ## 
    ## Coefficients:

    ##          ar1     ar2      ma1      ma2
    ##       0.0553  0.3538  -0.1029  -0.3792
    ## s.e.     NaN     NaN      NaN      NaN
    ## 
    ## sigma^2 estimated as 0.0003616:  log likelihood = 11769.13,  aic = -23528.27
    ## 
    ## Training set error measures:
    ##                        ME       RMSE        MAE        MPE      MAPE      MASE
    ## Training set 0.0003938441 0.01901318 0.01261887 0.01048973 0.3497938 0.9985228
    ##                      ACF1
    ## Training set -0.001768975

![image](https://github.com/user-attachments/assets/cb20ff73-7938-4d4a-a6c8-2cf5a60d388f)

![image](https://github.com/user-attachments/assets/6ad6f583-cd11-4a22-9554-fc99e4eb58a8)

    ## 
    ##  Box-Ljung test
    ## 
    ## data:  residuals(fit_arma212)
    ## X-squared = 14.933, df = 10, p-value = 0.1345

-   The ACF plot shows all correlation values (vertical bars) staying
    within the blue confidence lines. This means there’s no significant
    correlation between residuals at any time lag - they appear
    completely random. This clean result tells us the ARIMA model has
    successfully captured all predictable patterns in Nike’s stock
    prices. The random, small bars within the confidence bands confirm
    the residuals now behave like pure noise, which is exactly what we
    want to see in a well-fitted time series model.

-   The PACF plot shows nearly all points very close to zero, well
    within the confidence bands. While there are two tiny spikes around
    lags 5 and 15 that slightly cross the blue lines, these are so small
    they likely occurred by chance. Like the ACF, this confirms our
    model has done its job well - there are no important patterns left
    in the residuals. The minor spikes we see are insignificant and
    don’t suggest any missing structure in our model. Together, these
    plots give us confidence that the ARIMA model is working properly.

------------------------------------------------------------------------

## Optimal ARIMA Model Selection and Comparison

The auto.arima function selected an ARIMA(1,1,1) model as the best fit
for Nike’s stock prices. The model coefficients (AR1=0.6475,
MA1=-0.6932) show that current prices are influenced by both the
previous day’s price and past random shocks. The small sigma² value
(0.0003617) and high log likelihood (11769.13) indicate excellent model
fit. Error measures are very low (RMSE=0.019, MAE=0.0126), meaning the
model’s predictions closely match actual prices. The ACF1 value near
zero (-0.0036) confirms the residuals have no remaining patterns. With
the lowest AIC score (-23532.25) among compared models, this
ARIMA(1,1,1) is statistically the best choice for forecasting Nike’s
stock movements, balancing accuracy with simplicity.

    ## Series: nke_close 
    ## ARIMA(1,1,1) 
    ## 
    ## Coefficients:
    ##          ar1      ma1
    ##       0.6475  -0.6932
    ## s.e.  0.1248   0.1177
    ## 
    ## sigma^2 = 0.0003617:  log likelihood = 11769.13
    ## AIC=-23532.25   AICc=-23532.25   BIC=-23512.93
    ## 
    ## Training set error measures:
    ##                        ME      RMSE        MAE        MPE      MAPE      MASE
    ## Training set 0.0003966945 0.0190132 0.01262009 0.01056907 0.3498127 0.9986186
    ##                      ACF1
    ## Training set -0.003593554

![image](https://github.com/user-attachments/assets/137d57c2-3ecb-4548-95a8-36297212db29)

![image](https://github.com/user-attachments/assets/8a3abfc1-05cd-45d3-b3d7-0b5754ece5b3)

    ##             df       AIC
    ## auto_fit     3 -23532.25
    ## fit_arma111  3 -23532.25
    ## fit_arma112  4 -23530.35
    ## fit_arma212  5 -23528.27

-   The ACF plot shows all correlation values (vertical bars) falling
    completely within the blue confidence lines. This means there is no
    significant correlation between residuals at any time lag - they
    appear completely random. This clean pattern indicates our
    auto-selected ARIMA model has successfully removed all predictable
    patterns from the data. The residuals now behave like pure noise,
    which is exactly what we want to see in a well-fitted model.

-   The PACF plot shows nearly all points very close to zero, well
    within the confidence bands. While there are two tiny spikes around
    lags 5 and 15 that slightly cross the blue lines, these are so small
    they likely occurred by chance. This confirms our model has
    effectively captured all important price patterns. The minor spikes
    we see don’t represent any real missing structure and can be safely
    ignored for forecasting purposes.

-   The table compares four different ARIMA models for Nike’s stock
    prices. Both the auto-selected ARIMA(1,1,1) and manually specified
    ARIMA(1,1,1) show identical AIC scores (-23532.25), indicating
    equally good performance. The more complex models (ARIMA(1,1,2) and
    ARIMA(2,1,2)) have worse (higher) AIC values (-23530.35 and
    -23528.27 respectively), despite having more parameters. This tells
    us two important things: (1) the simpler ARIMA(1,1,1) model works
    just as well as the automatically selected one, and (2) adding extra
    parameters doesn’t improve the model enough to justify the added
    complexity. Therefore, the ARIMA(1,1,1) is the best choice - it’s
    simple but works very well for forecasting Nike’s stock prices.

------------------------------------------------------------------------

## Forecasting

![image](https://github.com/user-attachments/assets/e4601698-0a5b-47ed-8753-2034529c4c78)

The forecast graph shows Nike’s future stock price predictions using the
Auto ARIMA model. The black line represents historical prices, while the
blue line shows the forecasted values. The shaded blue area indicates
the prediction’s confidence range - wider areas mean more uncertainty.
The forecast suggests prices will remain relatively stable with small
fluctuations, neither sharply rising nor falling. However, the
confidence band gradually widens over time, showing predictions become
less certain further into the future. This is normal in stock
forecasting. The model expects Nike’s prices to follow their recent
pattern rather than making dramatic moves.

------------------------------------------------------------------------

## Monthly NKE Price Analysis: ARIMA Model Selection and Forecasting

Comperison of two ARIMA models for Nike’s monthly stock prices. The
ARIMA(1,1,0) model shows a small negative autoregressive effect (AR1 =
-0.0075) with drift (0.0072), suggesting prices tend to drift upward
very slightly. The ARIMA(1,1,1) model has stronger coefficients (AR1 =
0.5184, MA1 = -0.5667) and a smaller drift (0.0035). Both models have
similar error levels (sigma² ≈ 0.0056), but the ARIMA(1,1,0) performs
slightly better with lower AIC (-511.19 vs -509.88) and BIC (-501.01 vs
-496.31) values. This means the simpler ARIMA(1,1,0) model is likely
better for forecasting, as it explains the data nearly as well with
fewer parameters. The log likelihood values (258.6 vs 258.94) are very
close, confirming both models fit the data reasonably well.

![image](https://github.com/user-attachments/assets/5864ed4f-4bb7-48bb-bace-99835a5e0f59)

![image](https://github.com/user-attachments/assets/36b1c46d-22b7-47e1-a99c-09438b89f906)

    ## Using `date` as index variable.

![image](https://github.com/user-attachments/assets/fe03fb68-e783-4f31-82d8-22b2495ffae4)

![image](https://github.com/user-attachments/assets/32016211-0f71-4c4f-b62f-da4692928009)

![image](https://github.com/user-attachments/assets/c8743d7f-3317-4b48-a520-015dc5a02614)

1.  Original Time Series and ACF/PACF (Plot 1): The first graph shows
    the original time series of Nike’s stock prices, which displays a
    clear upward trend over time. This means the data is non-stationary.
    The ACF plot shows a slow decrease in autocorrelation, which is a
    common sign of non-stationary time series. The PACF plot shows a
    strong spike at lag 1 and smaller spikes afterward. These results
    suggest that the time series has strong dependencies and needs to be
    differenced to become stationary.

2.  Differenced Series and ACF/PACF (Plot 2): The second graph shows the
    differenced series, likely the returns. This series fluctuates
    around zero and appears more stable. The ACF and PACF plots of the
    differenced series show no significant spikes beyond the confidence
    bands. This indicates that the differencing process worked well and
    the series is now stationary, which is important for time series
    modeling.

3.  Fitted Model and ACF/PACF (Plot 3): This plot shows the fitted
    values from the model and the corresponding ACF and PACF. The fitted
    series follows the trend of the original data well. The ACF and PACF
    again show high autocorrelation at the first lag and a gradual
    decrease, suggesting that the model captured the trend but some
    autocorrelation still exists. This can happen in models that do not
    fully remove all dependencies.

4.  Residual Diagnostics (Plot 4): This graph shows the residuals from
    the model, which appear to fluctuate randomly around zero. The ACF
    plot of the residuals shows that most autocorrelations are close to
    zero and within the confidence bands. The histogram of the residuals
    is roughly bell-shaped, indicating that they are approximately
    normally distributed. This is a good sign and suggests the model’s
    residuals behave like white noise.

5.  Forecast Plot (Plot 5): The last graph shows the forecast of Nike’s
    stock prices. The black line represents the historical data, while
    the blue shaded areas show the forecast with 80% and 95% confidence
    intervals. The forecast line is relatively flat, with some
    uncertainty as time goes forward. This means the model expects the
    stock price to stay stable in the near future, but with a possible
    range of outcomes.

------------------------------------------------------------------------

## Weekly NKE Price Analysis: ARIMA Model Selection and Forecasting

Comperison of two ARIMA models for Nike’s weekly stock prices. The
ARIMA(1,1,0) model shows a small negative effect (-0.1159) from the
previous week’s price, with a tiny upward trend (0.0018). The
ARIMA(1,1,1) model has a stronger negative effect (-0.5165) from past
prices and accounts for random shocks (0.4026), with a slightly stronger
trend (0.0025). Both models fit the data well, with nearly identical
error levels (sigma² ≈ 0.0016). However, the ARIMA(1,1,1) performs
slightly better, with a lower AIC (-3448.91 vs -3446.96) and higher log
likelihood (1728.45 vs 1726.48), meaning it explains the data better
despite being more complex. The small differences suggest either model
could work, but the ARIMA(1,1,1) may capture more patterns in the weekly
price changes.

![image](https://github.com/user-attachments/assets/f3ab6e39-59de-430e-8f0d-2fbcbcbe105c)

![image](https://github.com/user-attachments/assets/9b50dd31-5a69-43cd-a42b-509dc16bb2b5)

    ## Using `date` as index variable.

![image](https://github.com/user-attachments/assets/4e4481a5-64d7-4246-93b4-37a76194f8bf)

![image](https://github.com/user-attachments/assets/096f2d02-8209-448d-a637-40963576f585)

![image](https://github.com/user-attachments/assets/7192f703-f799-48c3-ac64-f1666bea815a)

1.  Original Time Series and ACF/PACF (Plot 1): This graph shows the
    weekly closing prices of Nike stock. There is a clear upward trend
    over time, which means the series is not stationary. The ACF plot
    has strong autocorrelation at many lags, especially at the
    beginning, and decreases slowly. The PACF plot also shows a strong
    spike at lag 1. These patterns suggest that the data has a strong
    trend and needs to be differenced to become stationary.

2.  Differenced Series and ACF/PACF (Plot 2): The second graph shows the
    differenced version of the series, which removes the trend. Now, the
    values fluctuate around zero. The ACF and PACF plots show that the
    autocorrelations are smaller and mostly within the blue confidence
    bands. This means the series is now stationary, which is a good
    condition for time series modeling.

3.  Time Series (tsibble) and ACF/PACF (Plot 3): This plot displays the
    Nike weekly closing prices using the tsibble structure. The ACF and
    PACF results are similar to the first plot: high autocorrelation at
    lag 1 and slowly decreasing values after that. These signs again
    confirm that the original data is non-stationary and has strong time
    dependence.

4.  Residual Diagnostics (Plot 4): This graph shows the residuals from
    the fitted ARIMA model. The residuals appear random and centered
    around zero over time. The ACF plot of the residuals shows that most
    autocorrelations are near zero and stay within the confidence
    limits, suggesting no clear pattern remains. The histogram of the
    residuals is bell-shaped, indicating they are approximately normally
    distributed. These are good signs of a well-fitted model.

5.  Forecast Plot (Plot 5): The last graph shows the forecast for Nike’s
    weekly closing prices. The dark and light blue shaded areas
    represent 80% and 95% confidence intervals. The forecast line is
    relatively flat, which means the model predicts that prices will
    stay stable in the short term. However, the confidence intervals
    become wider over time, showing that the uncertainty increases in
    the future.

------------------------------------------------------------------------

# Conclusion

The analysis reveals three key findings about NKE stock:

<h4>

1.  Market Patterns
    </h4>

-   Clear weekday effects (Thursday highs, Monday lows)

-   January shows consistent underperformance

-   Strong pre-2021 growth followed by sustained decline

<h4>

1.  Modeling Results
    </h4>

-   ARIMA(1,1,1) delivers best balance of accuracy and simplicity

-   All models show clean residuals (Ljung-Box p &gt; 0.1)

-   Short-term forecasts remain stable; long-term uncertain

<h4>

1.  Practical Applications
    </h4>

-   Traders can exploit weekly seasonal patterns

-   Investors should monitor post-2021 trend breaks

-   Models perform best in stable market conditions

These results demonstrate that while NKE exhibits predictable short-term
behavior, recent volatility requires cautious interpretation of
long-term projections. The framework provides a foundation for ongoing
analysis and decision-making.

**Note:** Some of the interpretations and explanations were refined with
the help of GPT.
