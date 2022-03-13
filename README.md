# Credit Metrics Project

In this project using the CreditMetrics method I will calculate the credit VaR for bonds of the below mentioned countries. 
This method was published in 1997 in the form of a technical documentation by J.P. Morgan (in cooperation with e.g. Bank of Montreal, Bank of America, BZW, Deutsche Morgan Grenfell). 
It was designed to determine the value at risk of assets 

## Dataset
Historical data on 3-year bond quotes for four countries: Canada, the United Kingdom, the Philippines and Turkey, downloaded from https://pl.investing.com. 
This is monthly data from June 2012 to April 2019. The data includes the last bond value, the opening value, the maximum and minimum value, and the percentage change in the bond value for the month.

## Methodology
After creating a data frame containing monthly changes in bond values for 4 countries, I calculate their correlation.

To apply the Monte Carlo method, 50,000 scenarios were drawn from a multivariate normal distribution with a sigma parameter equal to the calculated correlation matrix.

The next step was to assign ratings to the generated values in the scenarios. For this purpose, for each country, using the transition matrix, ranges were created to assign ratings to the values in the scenarios. 

## Calculation of portfolio value
US$1,000,000 was invested in 3-year bonds from each of these countries. 
To calculate the value of the portfolio for each of the scenarios generated, I use a function I wrote that calculates the value of the bonds after the first year based on the average rates of return for bonds with the given ratings. 
If there is a D - bankruptcy rating, we calculate the value of the bonds for the country using a predetermined rate of return of 51.89%.

I then calculate the portfolio value, which is the sum of the bond values for each scenario, and the losses, which is the difference between the portfolio value if the bond ratings had not changed after one year and the values obtained under each scenario. 

The determined loss values were collected into a vector, sorted and 99.9% VaR was calculated. 
