# Ex.No-1B-CONVERSION-OF-NON-STATIONARY-TO-STATIONARY-DATA

## Date:11/03/2025

## AIM:
To perform regular differncing,seasonal adjustment and log transformatio on Rainfall Rate

## ALGORITHM:

1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal
adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log
transformation.
5. Display the overall results.

## PROGRAM:

## Import the necessary Packages
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```
## Load the dataset
```
train = pd.read_csv("/content/rainfall.csv")
```
## PLot the data without Conversion
```
train['date'] = pd.to_datetime(train['date'], format='%Y-%m-%d')  
train.set_index('date', inplace=True)  
train.head()
train['rainfall'].plot(title='Rainfall') 

def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)

adf_test(train['rainfall'])
```

## REGULAR DIFFERENCING
```
train['Rainfall_diff'] = train['rainfall'] - train['rainfall'].shift(1) 
train['Rainfall_diff'].dropna().plot(title='Differenced Rainfall Rate ')
```

## SEASONAL ADJUSTMENT
```
n = 7
train['Rainfall_seasonal_diff'] = train['rainfall'] - train['rainfall'].shift(n) 
train['Rainfall_seasonal_diff'].dropna().plot(title='Seasonally Differenced Rainfall Rate')
```

## LOG TRANSFORMATION
```
train['rainfall_log'] = np.log(train['rainfall'])
train['rainfall_log_diff'] = train['rainfall_log'] - train['rainfall_log'].shift(1)
train['rainfall_log_diff'].dropna().plot(title='Log Differenced Rainfall')
```

## OUTPUT:

## WITHOUT CONVERSION:
![image](https://github.com/user-attachments/assets/9db1674e-ae60-466e-8c76-f9d9aec0966c)

## REGULAR DIFFERENCING:
![image](https://github.com/user-attachments/assets/2d1f53e7-a0f0-49b5-b2d8-62811a4335b6)

## SEASONAL ADJUSTMENT:
![image](https://github.com/user-attachments/assets/05a20b09-b033-48bb-9100-76382d02b587)

## LOG TRANSFORMATION:
![image](https://github.com/user-attachments/assets/d611b06d-2cd7-4d32-9555-93ed8fffb83c)

