# Executive summary

## Research Question

Can a ARIMA model help improve timing of entry points into the S&P 500 and generate higher returns than a traditional Dollar Cost Averaging strategy?

## Introduction / Project Background

Typically, when people invest into the index, they will invest a set amount at the same time each month. This strategy is known as Dollar cost averaging (DCA). The idea of DCA is to reduce emotional decision making and smooth out volatility in the long run. Reference. This project will seek to explore whether using an ARIMA model to forecast S&P 500 data can be used as a baseline for timing investments throughout the month. This helps maintain the emotional decision-making aspect.

## Investment Methodology:

Each month, two ARIMA models forecast a high and low price for the next month using a rolling window approach. The strategy monitors daily closing prices and invests 75% of the monthly contribution on the first day the price is closer to the predicted low than the predicted high. The remaining 25% is invested at month-end. If no such day occurs, 100% is invested at the end of the month.

## Results

After the investment strategy has been applied, the two final amounts were compared. The normal DCA strategy returned $251,180, while the combined strategy utilising the ARIMA model returned $252,224, providing an extra $1043 over the 10-year period, investing $1000 each month.

## Next steps

To further evaluate ARIMA’s potential, alternative investment strategies can be tested to see if they outperform standard DCA by a statistically significant margin. Further analysis will explore whether ARIMA’s success was due to genuine predictive power or simply random market noise, diving deeper into when it succeeded and failed.

# Data Visuals and Analysis

To begin the analysis, a visual of the S&P 500 index monthly Lows/Highs were plotted on a line plot. This is to initially see overall trends, volatility and any seasonality. The visual is shown in figure 1.1 below.

 

Figure 1.1

<img width="1339" height="641" alt="image" src="https://github.com/user-attachments/assets/6feb92ba-e67b-4e20-bd75-81e246e1cc53" />

Figure 1.1 shows a strong upward trend, as expected, so differencing will have to be applied to ensure the data is stationary. With the periods of volatility from economic downturns such as the 2008 financial crisis and Covid, it makes it difficult to spot any seasonality visually. In absolute terms the data also shows larger variances as time goes on, suggesting a log transform will also have to be applied.

To assess seasonality and determine the appropriate ARIMA model parameters (p, d, q), the data was log-transformed and differenced to achieve stationarity. This was confirmed by an Augmented Dickey-Fuller test, which returned a near-zero p-value, indicating strong evidence of stationarity. ACF and PACF plots were then generated below for both models to guide the selection of model order and identify any seasonal patterns.

A graph with blue dots and numbers

AI-generated content may be incorrect.A graph of a function

AI-generated content may be incorrect.Figure 2.2 – Monthly High data

The two figures indicate no seasonality, likely ruling out the potential for seasonality to be used. Despite the studied seasonality in academic research, it is not prominent enough within the data to warrant using a SARIMA model. The plots also suggest order (1,1) for the (p,q) components.

The low data showed similar results in terms of seasonality but indicated order of (0,0) for the (p,q) components of the model.

A graph with blue dots and numbers

AI-generated content may be incorrect.Figure 2.3 – Monthly Low data

A graph with blue dots and numbers

AI-generated content may be incorrect.

 

When identifying the most optimal parameters, a grid search approach was used. This data was log transformed and each combination of (p,d,q) was used, being assessed by Akaike information criterion. The model with the lowest AIC was picked and resulted in the following parameters for each model showed in figure 2.4 below

Figure 2.4 – AIC and Parameters.

 

A screenshot of a computer screen

AI-generated content may be incorrect.

 

 

The grid search approach identified an optimal order for the ‘Low’ model that aligned with patterns observed in the ACF and PACF plots, yielding an AIC of -345.5, indicating strong model fit. For the ‘High’ model, the selected order differed from PACF suggestions but was chosen due to its lower AIC, prioritising statistical performance over visual diagnostics. Forecasts are shown in Figure 2.5. The use of AIC is considered best practice in time series model selection, as it balances model fit with complexity and helps avoid overfitting by penalising excessive parameters (Bevans, 2020).

Figure 2.5 – Forecast Vs Actuals Plot.

A graph of a graph

AI-generated content may be incorrect.

 

At a high level, to understand the accuracy common error metrics were used. The results are shown in figure 2.5 below.

Figure 2.6 – Error summary.

A white rectangular object with black text

AI-generated content may be incorrect.

 

 
Given the nature of the index, where price points movements increase over time, MAPE is used as the primary accuracy metric. The ‘Monthly Low’ model shows a higher error rate (3.63%) compared to the ‘Monthly High’ model (2%), largely due to sudden market crashes like Covid. These events tend to impact low values more sharply, whereas high values remain more stable. For example, in March 2020, the error was 30% for the low model versus 9% for the high. Despite this, the forecasts serve as bounds for investment decisions, so the impact of such errors is limited.

 
Further metrics were built such as the mean difference and the % of months where a cheaper price was observed compared to the DCA strategy. Results shown below in figure 2.7.

A screenshot of a computer

AI-generated content may be incorrect.Figure 2.7 – Error summary.

At an average level, the ARIMA based strategy got entry points 15.99 below the DCA strategy with 52.4% of the months being a cheaper price point.

Finally, over the 126-month period, the two strategies provided the following returns:

DCA – $126,000 invested at $1000 per month - $251,180.

ARIMA based strategy - $126,000 invested at $1000 per month - $252,224.

While ARIMA showed stronger performance on the surface, its statistical significance still needs to be tested. Past performance does not guarantee future results, and given the unpredictability of financial markets, these outcomes should be interpreted with caution.
