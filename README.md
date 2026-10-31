# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 31.10.2026

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load the Temperature Time Series Dataset
data = pd.read_csv('C:\\Users\\admin\\Downloads\\archive\\MLTempDataset1.csv')

print("Original Data:")
print(data.head())

# Extract temperature column
temperature = data['Hourly_Temp'].dropna().to_numpy()

# Calculate mean and variance
N = len(temperature)

lags = range(min(35, N))

autocorr_values = []

mean_data = np.mean(temperature)
variance_data = np.var(temperature)

# Go through lag components one by one
for lag in lags:

    if lag == 0:
        autocorr_values.append(1)

    else:
        auto_cov = np.sum(
            (temperature[:-lag] - mean_data) *
            (temperature[lag:] - mean_data)
        ) / N

        autocorr_values.append(auto_cov / variance_data)

# Display the graph
plt.figure(figsize=(10, 6))

plt.stem(lags, autocorr_values)

plt.title('Autocorrelation of Temperature Data')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')

plt.grid(True)
plt.tight_layout()
plt.show()

# Display autocorrelation values
print("\nAutocorrelation Values:")
for lag, value in zip(lags, autocorr_values):
    print(f"Lag {lag}: {value:.4f}")
```
### OUTPUT:
<img width="1278" height="947" alt="image" src="https://github.com/user-attachments/assets/b359e95c-2f57-433e-8f17-bc633316a93c" />

### RESULT:
Thus we have successfully implemented the auto correlation function in python.
