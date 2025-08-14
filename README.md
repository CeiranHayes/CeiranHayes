# Executive summary

## Research Question

Can a ARIMA model help improve timing of entry points into the S&P 500 and generate higher returns than a traditional Dollar Cost Averaging strategy?

## Introduction / Project Background

Typically, when people invest into the index, they will invest a set amount at the same time each month. This strategy is known as Dollar cost averaging (DCA). The idea of DCA is to reduce emotional decision making and smooth out volatility in the long run. This project will seek to explore whether using an ARIMA model to forecast S&P 500 data can be used as a baseline for timing investments throughout the month. This helps maintain the emotional decision-making aspect.

## Data Source
As the data being worked with is finanical data, it will be sourced from the 'yfinance' library within Python

## Investment Methodology:

Each month, two ARIMA models forecast a high and low price for the next month using a rolling window approach. The strategy monitors daily closing prices and invests 75% of the monthly contribution on the first day the price is closer to the predicted low than the predicted high. The remaining 25% is invested at month-end. If no such day occurs, 100% is invested at the end of the month.

## Results

After the investment strategy has been applied, the two final amounts were compared. The normal DCA strategy returned $251,180, while the combined strategy utilising the ARIMA model returned $252,224, providing an extra $1043 over the 10-year period, investing $1000 each month.

## Next steps

To further evaluate ARIMA’s potential, alternative investment strategies can be tested to see if they outperform standard DCA by a statistically significant margin. Further analysis will explore whether ARIMA’s success was due to genuine predictive power or simply random market noise, diving deeper into when it succeeded and failed.

# Data Visuals and Analysis

## Visualising the Index
To begin the analysis, a visual of the S&P 500 index monthly Lows/Highs were plotted on a line plot. This is to initially see overall trends, volatility and any seasonality. The visual is shown in figure 1.1 below.

 
*Figure 1.1*

<img width="693" height="503" alt="image" src="https://github.com/user-attachments/assets/35bc9218-9061-4769-a66e-58e6256f0e97" />


Figure 1.1 shows a strong upward trend, as expected, so differencing will have to be applied to ensure the data is stationary. With the periods of volatility from economic downturns such as the 2008 financial crisis and Covid, it makes it difficult to spot any seasonality visually. In absolute terms the data also shows larger variances as time goes on, suggesting a log transform will also have to be applied.

## PACF and ACF Plots
To assess seasonality and determine the appropriate ARIMA model parameters (p, d, q), the data was log-transformed and differenced to achieve stationarity. This was confirmed by an Augmented Dickey-Fuller test, which returned a near-zero p-value, indicating strong evidence of stationarity. ACF and PACF plots were then generated below for both models to guide the selection of model order and identify any seasonal patterns.


*Figure 2.2 – Monthly High data*

<img width="549" height="293" alt="image" src="https://github.com/user-attachments/assets/4960710d-b445-463c-880c-1f388e9514c9" /><img width="538" height="308" alt="image" src="https://github.com/user-attachments/assets/3aa58278-eb44-42ff-ae4b-7caad19190d4" />

The two figures indicate no seasonality, likely ruling out the potential for seasonality to be used. Despite the studied seasonality in academic research, it is not prominent enough within the data to warrant using a SARIMA model. The plots also suggest order (1,1) for the (p,q) components.

The low data showed similar results in terms of seasonality but indicated order of (0,0) for the (p,q) components of the model.

*Figure 2.3 – Monthly Low data*

<img width="554" height="350" alt="image" src="https://github.com/user-attachments/assets/ec4531e8-76a3-4ee5-98aa-d76ebb5e2444" />    <img width="592" height="303" alt="image" src="https://github.com/user-attachments/assets/e8683f46-9975-4914-b665-64c719dc2c9a" />
 

When identifying the most optimal parameters, a grid search approach was used. This data was log transformed and each combination of (p,d,q) was used, being assessed by Akaike information criterion. The model with the lowest AIC was picked and resulted in the following parameters for each model showed in figure 2.4 below

## Order Selection 
*Figure 2.4 – AIC and Parameters*

 
<img width="557" height="85" alt="image" src="https://github.com/user-attachments/assets/c3253b2e-70b2-48ec-ac23-8c95a70ca457" />

 

The grid search approach identified an optimal order for the ‘Low’ model that aligned with patterns observed in the ACF and PACF plots, yielding an AIC of -345.5, indicating strong model fit. For the ‘High’ model, the selected order differed from PACF suggestions but was chosen due to its lower AIC, prioritising statistical performance over visual diagnostics. Forecasts are shown in Figure 2.5. The use of AIC is considered best practice in time series model selection, as it balances model fit with complexity and helps avoid overfitting by penalising excessive parameters (Bevans, 2020).

## Visualising Results
*Figure 2.5 – Forecast Vs Actuals Plot*

At a high level, to understand the accuracy common error metrics were used. The results are shown in figure 2.5 below.
<img width="1339" height="641" alt="image" src="https://github.com/user-attachments/assets/6feb92ba-e67b-4e20-bd75-81e246e1cc53" />

## Understanding the accuracy and results
*Figure 2.6 – Error summary.*

<img width="380" height="73" alt="image" src="https://github.com/user-attachments/assets/a1f4dbd6-bafd-449d-a96f-4d0d8305c42d" />


 
Given the nature of the index, where price points movements increase over time, MAPE is used as the primary accuracy metric. The ‘Monthly Low’ model shows a higher error rate (3.63%) compared to the ‘Monthly High’ model (2%), largely due to sudden market crashes like Covid. These events tend to impact low values more sharply, whereas high values remain more stable. For example, in March 2020, the error was 30% for the low model versus 9% for the high. Despite this, the forecasts serve as bounds for investment decisions, so the impact of such errors is limited.

 
Further metrics were built such as the mean difference and the % of months where a cheaper price was observed compared to the DCA strategy. Results shown below in figure 2.7.

*Figure 2.7 – Error summary*
<img width="903" height="117" alt="image" src="https://github.com/user-attachments/assets/4b9264c9-42dd-4386-a981-11cb32a95133" />

At an average level, the ARIMA based strategy got entry points 15.99 below the DCA strategy with 52.4% of the months being a cheaper price point.

Finally, over the 126-month period, the two strategies provided the following returns:

DCA – $126,000 invested at $1000 per month - $251,180.

ARIMA based strategy - $126,000 invested at $1000 per month - $252,224.

While ARIMA showed stronger performance on the surface, its statistical significance still needs to be tested. Past performance does not guarantee future results, and given the unpredictability of financial markets, these outcomes should be interpreted with caution.
