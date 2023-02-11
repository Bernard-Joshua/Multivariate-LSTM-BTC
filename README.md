# Multivariate LSTM for hourly Bitcoin Prediction

# Introduction

This project is an optimized replica of my Final-Year project. The Final Year Project I have completed cannot be shared due to a privacy agreement with the company the project was for. The project involves using AI to make predictions on cryptocurrencies; Bitcoin, Polka-Dot, Ethereum and Cardano. The section below highlights the differences between my FYP and this project.


# Comparison

| Projects | U-Mobile Cryptocurrency Prediction Software | Replica |
| --- | --- | --- |
| Frontend | Django | None |
| Backend | Python, TensorFlow, SQL | Python, TensorFlow |
| Algorithm Used | Multivariate LSTM | Multivariate LSTM |
| Cryptocurrencies Supported | BTC, ETH, ADA, DOT | BTC |
| Optimization | Stochastic Gradient Descent | PCA, Drop-outs, Stochastic Gradient Descent, Batch-Shuffling, MI scores |
| Data-Split | 70% - Train, 30% - Test | 70% - Train, 10% Validation, 20% - Test. |
| Prediction Window | Previous 60 hrs batch used to predict 61st hour. | Previous 24 hrs used to predict 25th hour. |
| Final Model Accuracy ( MAPE ) | +/- 24% | +/- 5.67 % |


# Data and Features

There were no null values in the data, however there were values in the 0 range. These values were removed to prevent the model from getting confused. There are 6 features and 1 target. The target was the closing price. When evaluating the data, it showed that the High. Low and Open features had similar distributions with the target ( Close ). These four variables had almost similar means, standard deviations, and interquartile ranges, with each other. However, all their values fell within 2.5 deviations from the mean despite being positively skewed, hence no extreme value (outliers) and therefore had a confidence interval of 97.4% . The other two features were Volume BTC and Volume USD, both these features had positive skewness and outliers. However, the outliers were not removed because that could have effected the data due to the majority of the data having the outliers. Both these features also had low correlations with the target, with the Volume BTC have a low negative corelation of -0.33 and the Volume USD having a moderate positive correlation.


# Optimizations

Principal Component Analysis

A PCA was used to reduce the multicollinearity between the High, Low and Open features with the target. The results of the PCA showed that PC1 made up almost 99.999% of the variance of the dataset and consisted of a strong relationship between the High and Open features with the Close target.

MI Scores

MI scores or Mutual Information score algorithm was used to determine, the features importance based on the amount of information gained from each feature. The algorithms logic is similar to the logic behind decision trees. Based on the MI scores it was seen that the features PC1, High and Low were the best feature candidates for the model, since they had the highest information gain.

Batch Shuffling

Using the Scikit-Learn data splitting function the data was split at random in batches. Each batch contained a continuous set of the features for 24 hours, data on the PC1, High and Low from 1st to 24th hours of a particular date. However, the batches were randomized. Repeated overlap of these random batches with continuous data would cancel out the positive and negative randomness which in turn would weed out high variances and produce a more clean relationship between the features and the target.


# Final Score

The final score of the data which was measured with the metric; mean absolute percentage error indicated that the error rate was in the range of +/- 5.67 % which is pretty good given that the model was trained using only 32k+ records from 2018 -2022.


# Limitations

- Since the batches were randomized, I could not plot a time-series graph of the y and y-hat values. As a workaround I used a scatterplot which indicated a strong-positive correlation. However, if a linear-regression line was to be plotted then, only an 8th - order polynomial line would be able to fit.
- Could not create a dashboard to plot real-time values, the API's that produce hourly data are hidden behind pay-walls.
- Reshuffling the batches may produce different MAPE ranging from worst MAPE to better ones.


# Further Notes

- Graphs and Tables are available in the .ipynb file.
- Original Documents and their revisions for the FYP is available in the folders: Original & Revised Documents
- The revision of the design for the original project was done due to the cost involved in development on the Cloud. The Final Year Project did not give us a budget to work with.
