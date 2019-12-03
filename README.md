# Predicting Fish Mercury
# Research Question 
What is the relationship between soil geochemistry and mercury (Hg) in fish tissue in the United States?

## Dataset description
Data csv for soil geochemistry (n=64756): https://mrdata.usgs.gov/geochem/ and metadata available from: https://mrdata.usgs.gov/geochem/about.php

In this analysis only inductively coupled mass spectrometry- mass spectrometry (ICP-MS) chemical analysis results and select atomic absorption (AA) will be retained as independent variables.

Data csv for fish Hg (n=19705): https://www.epa.gov/fish-tech/national-survey-mercury-concentrations-fish-database-1990-1995

## Data Preparation
This spatial data required pre-processing. First a spatial data frame was developed from the imported csv files. Then a grid was developed to cover the United States (n=1534 cells). To aggregate the point data to the grid, where an average value was calculate per cell, a point to polygon aggregation was use on the NGS and Hg data. This attaches the ID of each cell a point lies in to the point layer. Then these layers were merged using a left join based on the grid ID. The data was then cleaned removing any cell that didn’t have all the data. 

## Scrub the Data
The data was cleaned by removing any by removing rows (grid cells) that had missing data. This left n=214.

## Variable selection
To avoid issues related to multicollinearity (highly correlated independent variables), independent variables that had a high correlation coefficient (r> ± 0.70) were removed. Then to ensure that a good relationship would be developed unnecessary predictors were removed. A variable was removed if the p-value of the correlation with the dependent variable was more than 0.20. This means that variables significant at an 80% confidence was retained. 

## Model
Linear regression, lasso, and ridge regression were compared. The performance of the models was very similar. The models were assessed using the root mean square error (RMSE) and mean absolute error (MAE). The R2 (unadjusted) was also used to quantify how much variance in the dependent variable could be explained by the independent variables. The ridge regression model was further tuned for final model presentation. 

Summary for the ridge regression:
RMSE = 0.228
MAE =  0.154
R2 = 0.04

## Conclusions/ recommendations
According to the best model produced by the Ridge Regression, all variables in the model exhibited a protective effect again the Hg body burden in fish. This mean that as the concentration of elements in the soil increase, the concentration of Hg in the fish tissue decrease. Molybdenum (-0.23) had the created influence on the concentration of Hg in the fish tissue, followed by copper (-0.22), lithium (-0.12), and thallium (-0.029). Further the ridge regression models had very low overall predictive power (4% variance explained). However, when these results were compared with the traditional statistical modelling with more user input into the model, difference results were obtained. Most concerning was the different direction of the coefficients. Additionally, the R2 was much higher in the ordinal least squares  (OLS) regression model. Thus, this leads me to conclude that a computer lead approach without expert input my provide a misspecified model. A combination of the two techniques would be recommended. 

Future Questions:
How do these patterns and relationships develop changed as we change how we aggregate the data to the grid.
1.	How does the grid location change the results?
2.	How does the type of grid chosen affect these results? Would a honeycomb grid have been better?
3.	How does the size of the grid change the results?



