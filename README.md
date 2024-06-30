# Portfolio-Allocation

This notebook focuses on asset selection in portfolio management, a major concern for many traders operating in financial markets. The primary objective of a financial portfolio is to maximize returns while minimizing risk, requiring a judicious allocation of assets. To achieve this, investors rely on existing theories, in particular the Modern Portfolio Theory (MPT) introduced by Harry Markowitz in 1950.

TMP emphasizes asset selection with the aim of maximizing returns while minimizing risk. The importance of diversification, based on uncorrelated assets, is emphasized to mitigate the impact of market shocks. The Markowitz correlation matrix offers a static view of asset relationships, ignoring the future evolution of correlations between them. Faced with this constraint, we seek to introduce a dynamic perspective by taking into account the evolution of asset relationships over time, including spillover effects (the propagation of the event from one sector to another) and feedback effects (where the situation has repercussions on itself).

To answer our problem, we will first start by presenting our database containing 147 S&P500 assets that we have previously transformed into returns. Then, we will use the Granger causality statistical test to establish our adjacency matrix based on a threshold, which will help us establish the causal relationships between our assets. This matrix will then be used to calculate our clusters using graph theory, based on Giorgio Fagiolo's article entitled "Clustering in Complex Directed Networks," written in 2007. These steps will allow us to select the least systemic assets that will constitute our portfolio to invest. Finally, we will conclude with a purchase and resale simulation on two periods : 2007 to 2010, and 2020 to 2022, thus evaluating the capacity of our model.

To deepen our analysis, we opted for a second approach to estimate causality between asset returns. This approach relies on using a machine learning model, specifically the Random Forest, to explore and exploit temporal relationships within financial time series. We created a function that takes financial return data as input. By applying the Random Forest method to each asset, we calculated the feature importance (lagged assets as explanatory variables) of each model associated with a specific asset to construct an adjacency matrix, thus representing the causality between each asset return in a temporal context. For this, the "feature_importances_" method of the RandomForestRegressor was used. It is worth noting that we took care to normalize the feature importance scores to allow for a more intuitive comparison between different features.

<br><br>
# Results 
<br><br>
We have decided to look at the impact only of periods when financial crises have occurred: the 2008 crisis and COVID-19. We are looking to see how our model will act in the face of these crises. We will start by looking at the results over a calculation period of 22 days (1 month in trading) and then, depending on the results obtained, we will invest in the following 10 days. A 30-day interval will allow us to assess the ability of our model to quickly adjust to changing market conditions. Investing in the following 10 days after the calculation period can be justified by our desire to see rapid decision-making. In addition, to enrich our analysis, we have decided to add the calculation of the Sharpe ratio. Indeed, the periods we have selected are characterized by significant volatility and market uncertainties. The Sharpe ratio will therefore allow us to assess the extent to which our model manages to generate a risk-adjusted return, thus providing crucial insights into its robustness during periods of financial crises.
<br><br>

### 1. Clustering method : 
#### A. 2008 to 2010 : 
<br><br>

<p align="center">
<img width="330" alt="Capture d’écran 2024-06-30 à 10 26 21" src="https://github.com/Mayslimani1/Portfolio-Allocation/assets/154423073/574cb921-96a4-489c-8962-077f1f4fc349">
  <br>
  <em style="font-size: 14px; color: black;"> Results of the purchase/resale simulation over a calculation period of 22 days and an investment period of 8 days between 2008 and 2010.</em>
</p>
<br><br>

The buy-sell simulation for this period reflected the severity of the crisis with a sharp drop in returns for the year 2008.
Following the implementation of our strategy, we can see that the Sharpe Ratio was negative for the majority of investment periods. This means that the portfolio-adjusted return is lower than the risk-free rate, indicating that the investor could have performed better if he had invested in risk-free assets. However, given the context of the time, these results were expected. The positive Sharpe Ratios nevertheless indicate that we managed to limit some losses.


<p align="center">
<img width="500" alt="Capture d’écran 2024-06-30 à 10 11 07" src="https://github.com/Mayslimani1/Portfolio-Allocation/assets/154423073/a0595dad-2b50-4ca2-b70e-16e034c84a2b">
    <br>
  <em style="font-size: 14px; color: black;"> Evolution of capital after investment for the period 2007 to 2008 of the S&P500.</em>
</p>

#### B. 2020 to 2022 : 
<br><br>

<p align="center">
<img width="334" alt="Capture d’écran 2024-06-30 à 10 31 35" src="https://github.com/Mayslimani1/Portfolio-Allocation/assets/154423073/24125481-23b7-4b70-bf19-cdb1ef000feb">
    <br>
  <em style="font-size: 14px; color: black;"> Results of the purchase/resale simulation over a calculation period of 22 days and an investment period of 8 days between 2020 and 2022.</em>
</p>
<br><br>

The period from 2020 to 2022 was marked by an economic response from governments and central banks to the challenges posed by the COVID-19 pandemic. Monetary policy, led by central banks, played a crucial role in stabilizing financial markets and stimulating the economy. The US Federal Reserve, for example, adopted accommodative monetary policies, lowering interest rates to historically low levels to encourage borrowing and investment. The S&P 500, a leading indicator of the US stock market, benefited from these policy interventions, recording strong growth in returns during this period. Despite the economic recession during this period, the return on our assets has continued to grow to date, with a portfolio value exceeding $1,250 after January 2022.
<br><br>

<p align="center">
<img width="500" alt="Capture d’écran 2024-06-30 à 10 12 28" src="https://github.com/Mayslimani1/Portfolio-Allocation/assets/154423073/39e1876a-9d85-4022-9bc2-ca9fe185f8ca">
    <br>
  <em style="font-size: 14px; color: black;"> Evolution of capital after investment for the period 2020 to 2022 of the S&P500.</em>
</p>
<br><br>

### 1. Machine learnig method : Random Forest 


The results of this method seem to be very similar to the first tested. Indeed, the periods of decline for both methods are identical. However, during the two crisis periods, the first model loses much more money during the peak of decline than the second, but also regains much more. Indeed, we see for example that during the month of October 2008, the capital is worth approximately $910 against $970 for the Random Forest. The same observation is made for the COVID-19 period, where the peak of loss of March 2023 is represented by a capital of $920 for the first method and $985 for the second, without regaining as much afterwards.

<br><br>

#### A. 2008 to 2010 : 

<p align="center">
<img width="500" alt="Capture d’écran 2024-06-30 à 10 11 33" src="https://github.com/Mayslimani1/Portfolio-Allocation/assets/154423073/b99c54a8-c232-4d7b-9a59-ce3a123192f9">
  <br>
  <em style="font-size: 14px; color: black;"> Evolution of capital after investment for the period 2008 to 2010 of the S&P500.</em>
</p>

<br><br>

#### B. 2020 to 2022 : 

<p align="center">
<img width="500" alt="Capture d’écran 2024-06-30 à 10 12 46" src="https://github.com/Mayslimani1/Portfolio-Allocation/assets/154423073/3d91d4b3-8470-4073-b13e-5a6b593a865f" >
  <br>
  <em style="font-size: 14px; color: black;"> Evolution of capital after investment for the period 2020 to 2022 of the S&P500.</em>
</p>

<br><br>

# Conclusion :

The first model is therefore "riskier" than the second, because it reacts more sensitively to exogenous shocks. A risk-averse investor will therefore rather favor the second method.

The first method, based on the calculation of Granger causality, showed superior performance in terms of gains, but also increased sensitivity in times of crisis compared to the causality method with random forest regression, which showed a slight reduction in risk during these difficult periods. These two approaches, although different, showed similarities due to the use of graph theory in the calculation of the clustering coefficient.


