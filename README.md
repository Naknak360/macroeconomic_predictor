# Macroeconomic Factors and Their Impacts on the S&P 500

**Link to Jupyter Notebook:** [Explore the analysis](./macroeconomic_predictor.ipynb)

## Project Overview
This project seeks to characterize the effects of macroeconomic factors on the S&P 500. I will be exploring a variety of different models to see which one most accurately forecasts the S&P 500 and therefore gives the best insight into which macroeconomic factor plays the biggest role in influencing the market. I believe this project is important because I would like to bring more detailed analysis and awareness to the commonfolk about what to look out for in terms of macroeconmic news and what might positively or negatively affect their investments in the top 500 companies of the United States. 

## Findings 
Based on all of the research I conducted, the best model, albeit still terrible, at forecasting the S&P 500 was my Ridge regression model. This model happened to be the only one that had a positive R^2 score on the test set and had the lowest RMSE and MAE at 1359 and 940 respectively. The worst model, to my surprise, was the XGboost model which grossly overfit the training set with an R^2 score of 0.9999999999932732 while having a very negative R^2 score for the test set. Having almost a perfect R^2 score for the training set means that XGBoost learned all of the noise and almost 100% accurately predicted the S&P 500 values while performing terribly on unseen data. Below is a summary of all of my models and their performances:

### LASSO:

LASSO Train Performance: {'RMSE': 91.80226131648229, 'MAE': 67.53227703787371, 'R2': 0.9589269136334477}

LASSO Test Performance: {'RMSE': 1929.9310283830443, 'MAE': 1416.552133918074, 'R2': -0.8447774027906134}

Coefficients: [  0.          -0.          -0.          -0.           0.
 194.49734308  41.7821174   -0.           0.         -30.44929644
   0.           0.           0.          20.25328726  -0.
  -0.          -0.          -0.          -0.           0.
  -0.           0.         -14.98842554   0.          62.88131163
   0.          -0.           0.          -0.           0.
   0.           0.           0.          -0.           0.
  -0.          -0.          -0.           0.          -0.
   0.          -0.           0.          56.69366349   0.
  -0.           0.          -0.           0.           0.
   0.           0.          -0.           0.          -0.
  -0.          -0.           0.         -53.6521794    0.
  -8.88355061   0.          53.58051457   0.          -0.
   0.          -0.           0.           0.           0.
  20.66329268  -0.           0.          -0.          -0.
  -0.        ]

### Ridge:

Ridge Train Performance: {'RMSE': 124.56420887881193, 'MAE': 88.07296989936324, 'R2': 0.924379920700002}

Ridge Test Performance: {'RMSE': 1359.310139412177, 'MAE': 940.9801499565093, 'R2': 0.0848389962625068}

Coefficients: [  8.21627102 -10.38444583   0.54913844  -7.6628366    9.20105448
  16.63972751  10.86213209   1.9250834    8.22093203 -11.65845492
   8.21636359  12.47267577  11.0177546    7.44308061  -0.02513803
   0.21248854   6.64513444  -5.34346254   1.79686376   8.22797772
 -10.93898112   1.18748368  -7.71485778   9.11839236  16.69703546
   9.93126746   1.53405977   8.21910231 -11.39406446   8.2304973
  12.47124039  11.19998703   6.8387486    0.4506035    0.80805241
   6.66756167  -5.49941499   1.9881221    8.24312195 -11.50802175
   1.83592204  -7.73104284   9.03494904  16.74738101   9.35813117
   1.17771052   8.19805812 -11.15001069   8.24656579  12.47615314
  11.36320058   6.32693689   0.94816976   1.43625189   6.69339192
  -5.66403853   2.17952988   8.25253943 -12.07512685   2.44791489
  -7.81138676   8.95560532  16.80007854   8.9254634    1.04811419
   8.1393146  -10.87377024   8.25180879  12.46153033  11.53338918
   5.90371852   1.39547784   1.98643621   6.71590959  -5.89617861
   2.36266717]

### Random Forest:

Random Forest Train Performance: {'RMSE': 18.50915437426967, 'MAE': 10.962333351210031, 'R2': 0.9983303565598349}

Random Forest Test Performance: {'RMSE': 1946.9320689118103, 'MAE': 1436.338600227004, 'R2': -0.877422379339134}

### XGBoost:

XGBoost Train Performance: {'RMSE': 0.001174841412475891, 'MAE': 0.0008906552111767382, 'R2': 0.9999999999932732}

XGBoost Test Performance: {'RMSE': 1959.8733002525753, 'MAE': 1453.1182017103533, 'R2': -0.9024637311567143}

## Conclusion
As we can see from all four of my model choices (LASSO, Ridge, Random Forest, and XGBoost), we are not seeing anything indicating good modeling performance. This is even after using GridSearchCV in all of my pipelines which would ideally be tuning all of my hyperpareameters. I also made sure to standardize and scale all of my features to ensure that no one feature overshadows another in sheer magnitude. In all of my attempts to model the data, I experienced good training perfomance in RMSE, MAE, and R^2 score, but I witnessed the exact opposite for the test set performance of the models. The RMSE and MAE were drastically higher (in LASSO and Random Forest it was degree 2 difference), and the R^2 score for all of the models on the test set were in the negatives (except for Ridge regression which had a very slightly positive R^2 score). A negative R^2 score indicates that the model is performing worse than a baseline model that would simply predict the mean of the target variable. This means that all of the models are not drawing any significant meaning or correlation from the feature space to the target variable we are trying to predict, and instead, it seems as if all of the models are overfitting the noise of the training set. My claim that there is terrible overfitting at play is exemplified by my XGBoost model which shows a very high R^2 score of 0.99999 which is almost nearly 1 which means that the model is almost perfectly predicting the target variable values. 

Despite the poor performance witnessed by all of my models at trying to predict S&P 500 data based on macroeconomic factors alone, I can still draw very meaningful conclusions from my work. First, the most apparent conclusion is that it is very hard and almost impossible to forecast the S&P 500 based solely on macroeconomic factors provided by the Federal Reserve Bank of St. Louis. I had done lots of research and data filling to try and make the macroeconomic factors added to the feature space as predictive of the S&P 500 as possible, but the results listed above are evidence enough that there needs to be supplemental data to reinforce the features. I will admit that there is still room for me to optimally clean the target variable and feature space, but I think that with how noisy the markets are by nature, it is impossible to rid the data of all noise completely. That leads me to my next point: the stock markets being so noisy may have contributed to the overfitting seen by all of my models. Given the very high R^2 scores on the training sets vs the negative R^2 scores on the test sets, I can conclude that the models are all overfitting and are trying to factor too much of the noise into their predictions. After further research, I believe some ideas like statistical arbitrage might be a good way to better predict and model the noise in the S&P 500 as this method quntitatively describes mispricings in the market and may allow my model to get a better idea of the direction of smaller price movements/noise. 

Another thing to note is that for my linear regression models (LASSO and Ridge), they both associated the highest positive correlation between the Industrial Produciton Index feature and the S&P 500 while the strongest negative correlation is between the Unemployment Rate feature (lagged by 3 months) and the S&P 500. This conclusion was drawn based on their coefficient matrices.

If I were to expand on this project in the future, my next goals would be to expand the research question I posed. Rather than trying to predict the S&P 500 based only on macroeconomic factors, I would try to predict the S&P 500 based on more features such as public sentiment, statistical arbitrage, and other quantitative trading strategies to see if any of these categories are better forecasters of the market. 

I think that if this task were as simple as me modeling it just by macroeconomic factors alone, more people would have less confusion over the markets and I imagine more people could get rich off of day trading. However, the reality is that the market is difficult to model, and prices fluctuate for a plethora of reasons. Being able to track all of these changes and find out which feature would be the best predictor of said changes is a daunting task, but that is my recommendation for where I would take this task next. 