# Commercial-Real-Estate-(CRE)-Loan-Credit-Risk-Model
## Background
US CRE mortgage market consists of around $4.5 trillion of loans. The banking industry only hold 45% of the CRE loans.  The 25 largest banks by total assets hold 13% of all CRE mortgages, while the 4,600 banks outside the largest 100 hold 15–20% of all CRE mortgages. <br> <br>
Unlike Commercial and Industrial (C&I) loan or retail loan, the borrowers of CRE loan are usually corporate entities that are not rated by any of the big three rating agencies (Standard and Poor's, Fitch, Moody). This make CRE loan usually does not have credit rating or credit score like C&I or retail loan. As there are no credit rating or credit score available, most small bank adopt their own qualitative approaches in evaluating credit risk in CRE loan, which could lead to inaccuracy and inconsistency in credit risk management. <br> <br>
Therefore, it is important to build a scientific and accurate model in predicting credit risk in CRE loan. As there are several CRE Real Estate Investment Trusts(REIT) ETF with credit rating available, there is an opportunity of using the credit rating and financial performance of those ETF to build a model in predicting credit risk in different CRE loans.

## Method
### Data collection and transformation
This project first acquired financial performance from 2023 Q3 10-Q forms along with the latest credit ratings of the REIT. Then converting the EBITDA, Interest Expenses, Cash, Total Liabilities, Total Equities, Total Assets into Interest Expense Coverage Ratio, Net Debt Leverage Ratio, Total Leverage Ratio, Debt to Equity Ratio, EBITDA Asset Ratio, and EBITDA to Equity Ratio. Next, it will convert the credit rating into 5 year accumulated default rate based on the Default, Transition, and Recovery: 2022 Annual Global Corporate Default And Rating Transition Study by Standard and Poor's. <br>

### Model building
A 60-40 train test split will first be applied to the dataset(The number of data sample is not enough to do 70-30 split). In order to capture different types of non-linear relationship between predictors and default rate, the project will first regress the default rate with predictors, squared form of predictors, and logged form of predictors. Then a backward elimination by AIC will be performed to kick out the predictors that are lack of explaining power in the model. Then evaluate the MAE of the model to see how much difference the predicted default rate and the estimated default rate from credit rating is. <br><br>
If the MAE on the testing dataset is not satisfactory, it could imply an over-fitting occurs due to the large number of predictors. In that case, an elastic net regression will be performed to prevent over-fitting.

## Return for R code
Summary of Multiple Regression<br>
![image](https://github.com/HaHaIamHarry/Commercial-Real-Estate-CRE-Loan-Credit-Risk-Model/assets/141811361/a53a1ce3-55e1-4274-940b-5e25b987bb67)
<br>MAE and RMSE of Multiple Regression<br>
<br>"The MAE for training dataset:  0.00352602822602858"
<br>"The MAE for testing dataset:  0.0969951846377991"
<br>"The RMSE for training dataset:  0.00444128798272727"
<br>"The RMSE for testing dataset:  0.350579093907196"

Coefficient of Elastic Net Regression<br>
![image](https://github.com/HaHaIamHarry/Commercial-Real-Estate-CRE-Loan-Credit-Risk-Model/assets/141811361/8813f43e-855a-4f82-8f63-0353b9f31d68)
<br>MAE and RMSE of Elastic Net Regression<br>
<br>"The MAE for training dataset:  0.00566358952474341"
<br>"The MAE for testing dataset:  0.01444799039815"
<br>"The RMSE for training dataset:  0.0076190505684831"
<br>"The RMSE for testing dataset:  0.0302670576314153"

## Result and limitation
The result shown a big improvement in MAE from multiple regression(9.70% MAE in default rate) to elastic net regression(1.44% MAE in default rate). However, the current model (1.44% MAE and 3.03% RMSE) is still not perfect enough due to the lack of data sample. Currently, the author does not have Refinitiv or Bloomberg terminal on hand, once those tools are available, the data sample can be enlarged by putting in different years of financial figures and credit rating of the 48 REITs.

## Reference
S&P Global Ratings. (2023, April 25). Default, Transition, and Recovery: 2022 Annual Global Corporate Default And Rating Transition Study. S&P Global. Retrieved from https://www.spglobal.com/ratings/en/research/articles/230425-default-transition-and-recovery-2022-annual-global-corporate-default-and-rating-transition-study-12702145 <br>
Cohen & Steers. (2023, March). The commercial real estate debt market: Separating fact from fiction. Retrieved from https://www.cohenandsteers.com/insights/the-commercial-real-estate-debt-market-separating-fact-from-fiction
