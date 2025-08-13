Executive summary

Research Question

Can a ARIMA model help improve timing of entry points into the S&P 500 and generate higher returns than a traditional Dollar Cost Averaging strategy?

Introduction / Project Background

Typically, when people invest into the index, they will invest a set amount at the same time each month. This strategy is known as Dollar cost averaging (DCA). The idea of DCA is to reduce emotional decision making and smooth out volatility in the long run. Reference. This project will seek to explore whether using an ARIMA model to forecast S&P 500 data can be used as a baseline for timing investments throughout the month. This helps maintain the emotional decision-making aspect.

Investment Methodology:

Each month, two ARIMA models forecast a high and low price for the next month using a rolling window approach. The strategy monitors daily closing prices and invests 75% of the monthly contribution on the first day the price is closer to the predicted low than the predicted high. The remaining 25% is invested at month-end. If no such day occurs, 100% is invested at the end of the month.

Results

After the investment strategy has been applied, the two final amounts were compared. The normal DCA strategy returned $251,180, while the combined strategy utilising the ARIMA model returned $252,224, providing an extra $1043 over the 10-year period, investing $1000 each month.

Next steps

To further evaluate ARIMA’s potential, alternative investment strategies can be tested to see if they outperform standard DCA by a statistically significant margin. Further analysis will explore whether ARIMA’s success was due to genuine predictive power or simply random market noise, diving deeper into when it succeeded and failed.
