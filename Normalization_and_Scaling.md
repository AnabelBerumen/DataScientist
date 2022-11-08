```python
# modules we'll use
import pandas as pd
import numpy as np

# for Box-Cox Transformation
from scipy import stats

# for min_max scaling
from mlxtend.preprocessing import minmax_scaling

# plotting modules
import seaborn as sns
import matplotlib.pyplot as plt

# set seed for reproducibility
np.random.seed(0)
```
### Scaling vs Normalization
![](https://lh3.googleusercontent.com/HYYaWfQLnk5HLW_rtRcSRmKwBFpn4VRSEigjoJgEYrt3CC-EZkVE38mijNpBZJOFUibaYL8SxA7YqrBT8ilDLftxzF4bHk5vBKfC9CzB42ccBq7vmOUDchh3mb9TjNRcP-Z3x4iD)

## Scaling
### in scaling, you're changing the range of your data.
This means that you're transforming your data so that it fits within a specific scale, like 0-100 or 0-1. You want to scale data when you're using methods based on measures of how far apart data points are, like support vector machines (SVM) or k-nearest neighbors (KNN). With these algorithms, a change of "1" in any numeric feature is given the same importance

```python
# generate 1000 data points randomly drawn from an exponential distribution
original_data = np.random.exponential(size=1000)

# mix-max scale the data between 0 and 1
scaled_data = minmax_scaling(original_data, columns=[0])

# plot both together to compare
fig, ax = plt.subplots(1, 2, figsize=(15, 3))
sns.histplot(original_data, ax=ax[0], kde=True, legend=False)
ax[0].set_title("Original Data")
sns.histplot(scaled_data, ax=ax[1], kde=True, legend=False)
ax[1].set_title("Scaled data")
plt.show()
```
![Visualization](https://www.kaggleusercontent.com/kf/82374396/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..xa4ARCtTw_EYS8_xWJlfLA.AkMK_P3l3bE5-gwNiSKWUydsBsn96WEd4EyraYiUa1UJypWHngFnVohHGR4_iIIeUYcrpJ8NvAv2Vr_UlziQdBwsZK-Ozkwq9eVp16yoBHyM4cNwPNixQeSfp2XOpSA5xun_WdZilhONzPahlhhisqXoSZBF3oBF75HJqAMWfZqhwYWMAxZy6pZbj08ZSQUZGghbKngMzRfvGRNu4_hUiF20fkkhjBCyomeGxETUs0yoBdY6OW29bb1fxaiCcmOinifGMoH7mxlc0Bimj9AHn3NRYB8tZ85vzgvKgd4YPPOqpLhnfbbIeF1U0VdaNNJeJSCKNpyT1jBLdiOumMp3vpcLsK24FK16oULI2izl-E_avxawjoR5JOPr451G6Ci66BMo5vcZjwkGVb-AynsKF1kaa9TksNaJ-Aqm02Hor8_9MFWu3FBTdu8GMQJN5P5pfgA6JphBv4QuHLuHNtNQ7-CAkiA0erWnoBjHxtF985Azoifvbed6EWGR3HbvXVRXfjYOvbnUIZFgvIgacU5IbWPRht2_bV-zbxRhVJSZ3hbqmWZ7RGFhM6_A86aBkLBVKN8s-5jeVRkrtX-Bi955rpQtrhXv6PWU3JafpJsWxYAcIoytekAsMD9TjwOoUtdwV8eFOoH7656EKVcqaNPIwdE_zfLIwL6N1xjscINud9U.r4c2LW4TD6JbNTfNhmp-0g/__results___files/__results___4_0.png)


## Normalization
### in normalization, you're changing the shape of the distribution of your data.
The point of normalization is to change your observations so that they can be described as a normal distribution.

Normal distribution: Also known as the "bell curve", this is a specific statistical distribution where a roughly equal observations fall above and below the mean, the mean and the median are the same, and there are more observations closer to the mean. The normal distribution is also known as the Gaussian distribution.

```python
# normalize the exponential data with boxcox
normalized_data = stats.boxcox(original_data)

# plot both together to compare
fig, ax=plt.subplots(1, 2, figsize=(15, 3))
sns.histplot(original_data, ax=ax[0], kde=True, legend=False)
ax[0].set_title("Original Data")
sns.histplot(normalized_data[0], ax=ax[1], kde=True, legend=False)
ax[1].set_title("Normalized data")
plt.show()
```
![Visualization](https://www.kaggleusercontent.com/kf/82374396/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..xa4ARCtTw_EYS8_xWJlfLA.AkMK_P3l3bE5-gwNiSKWUydsBsn96WEd4EyraYiUa1UJypWHngFnVohHGR4_iIIeUYcrpJ8NvAv2Vr_UlziQdBwsZK-Ozkwq9eVp16yoBHyM4cNwPNixQeSfp2XOpSA5xun_WdZilhONzPahlhhisqXoSZBF3oBF75HJqAMWfZqhwYWMAxZy6pZbj08ZSQUZGghbKngMzRfvGRNu4_hUiF20fkkhjBCyomeGxETUs0yoBdY6OW29bb1fxaiCcmOinifGMoH7mxlc0Bimj9AHn3NRYB8tZ85vzgvKgd4YPPOqpLhnfbbIeF1U0VdaNNJeJSCKNpyT1jBLdiOumMp3vpcLsK24FK16oULI2izl-E_avxawjoR5JOPr451G6Ci66BMo5vcZjwkGVb-AynsKF1kaa9TksNaJ-Aqm02Hor8_9MFWu3FBTdu8GMQJN5P5pfgA6JphBv4QuHLuHNtNQ7-CAkiA0erWnoBjHxtF985Azoifvbed6EWGR3HbvXVRXfjYOvbnUIZFgvIgacU5IbWPRht2_bV-zbxRhVJSZ3hbqmWZ7RGFhM6_A86aBkLBVKN8s-5jeVRkrtX-Bi955rpQtrhXv6PWU3JafpJsWxYAcIoytekAsMD9TjwOoUtdwV8eFOoH7656EKVcqaNPIwdE_zfLIwL6N1xjscINud9U.r4c2LW4TD6JbNTfNhmp-0g/__results___files/__results___6_0.png)
