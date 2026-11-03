# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 03/10/2026

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.

### DATASET
DailyDelhiClimate 

### SOFTWARE REQUIRED
Jupyter Notebook

### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
# Load the dataset (train + test combined into one continuous daily series)
train = pd.read_csv('DailyDelhiClimateTrain.csv', parse_dates=['date'])
test = pd.read_csv('DailyDelhiClimateTest.csv', parse_dates=['date'])
df = pd.concat([train, test]).sort_values('date').reset_index(drop=True)
column = 'meantemp'
data = df[column].values
N = len(data)
lags = range(35)
```
```python
#Pre-allocate autocorrelation table
autocorr_values = []

#Mean
mean_data = np.mean(data)
#Variance
variance_data = np.var(data)
#Normalized data
normalized_data = (data - mean_data) / np.sqrt(variance_data)
#Go through lag components one-by-one
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum((data[:-lag] - mean_data) * (data[lag:] - mean_data)) / N
        autocorr_values.append(auto_cov / variance_data)  # Nor
#display the graph
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)
plt.title(f'Autocorrelation of Delhi Daily {column}')
plt.xlabel('Lag (days)')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()
```

### OUTPUT:
<img width="1099" height="553" alt="image" src="https://github.com/user-attachments/assets/cf5e20bf-9c31-4179-bb4f-dd55d5fa77bb" />

### RESULT:
 Thus we have successfully implemented the auto correlation function in python.
