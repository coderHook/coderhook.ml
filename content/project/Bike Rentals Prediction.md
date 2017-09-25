+++
# Date this page was created.
date = "2017-04-27"

# Project title.
title = "Bike Rentals Prediction"

# Project summary to display on homepage.
summary = "Using tecnics of machine learning we are going to predict how many Bikes do we need in order to give a service in a specific town."

# Optional image to display on homepage (relative to `static/img/headers` folder).
image_preview = "rental-bikes.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["datascience"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "headers/rental-bikes.jpg"
caption = "Predicting the apropiate number of bikes that we will need in order to provide the service :smile:"

+++



```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

bike_rentals = pd.read_csv("bike_rental_hour.csv")

print(bike_rentals.head())
```

       instant      dteday  season  yr  mnth  hr  holiday  weekday  workingday  \
    0        1  2011-01-01       1   0     1   0        0        6           0   
    1        2  2011-01-01       1   0     1   1        0        6           0   
    2        3  2011-01-01       1   0     1   2        0        6           0   
    3        4  2011-01-01       1   0     1   3        0        6           0   
    4        5  2011-01-01       1   0     1   4        0        6           0   

       weathersit  temp   atemp   hum  windspeed  casual  registered  cnt  
    0           1  0.24  0.2879  0.81        0.0       3          13   16  
    1           1  0.22  0.2727  0.80        0.0       8          32   40  
    2           1  0.22  0.2727  0.80        0.0       5          27   32  
    3           1  0.24  0.2879  0.75        0.0       3          10   13  
    4           1  0.24  0.2879  0.75        0.0       0           1    1  



```python
plt.hist(bike_rentals['cnt'])
plt.show()
```

![jpg](/img/ds/bike/output_1_0.png)


```python
bike_rentals.corr()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>instant</th>
      <th>season</th>
      <th>yr</th>
      <th>mnth</th>
      <th>hr</th>
      <th>holiday</th>
      <th>weekday</th>
      <th>workingday</th>
      <th>weathersit</th>
      <th>temp</th>
      <th>atemp</th>
      <th>hum</th>
      <th>windspeed</th>
      <th>casual</th>
      <th>registered</th>
      <th>cnt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>instant</th>
      <td>1.000000</td>
      <td>0.404046</td>
      <td>0.866014</td>
      <td>0.489164</td>
      <td>-0.004775</td>
      <td>0.014723</td>
      <td>0.001357</td>
      <td>-0.003416</td>
      <td>-0.014198</td>
      <td>0.136178</td>
      <td>0.137615</td>
      <td>0.009577</td>
      <td>-0.074505</td>
      <td>0.158295</td>
      <td>0.282046</td>
      <td>0.278379</td>
    </tr>
    <tr>
      <th>season</th>
      <td>0.404046</td>
      <td>1.000000</td>
      <td>-0.010742</td>
      <td>0.830386</td>
      <td>-0.006117</td>
      <td>-0.009585</td>
      <td>-0.002335</td>
      <td>0.013743</td>
      <td>-0.014524</td>
      <td>0.312025</td>
      <td>0.319380</td>
      <td>0.150625</td>
      <td>-0.149773</td>
      <td>0.120206</td>
      <td>0.174226</td>
      <td>0.178056</td>
    </tr>
    <tr>
      <th>yr</th>
      <td>0.866014</td>
      <td>-0.010742</td>
      <td>1.000000</td>
      <td>-0.010473</td>
      <td>-0.003867</td>
      <td>0.006692</td>
      <td>-0.004485</td>
      <td>-0.002196</td>
      <td>-0.019157</td>
      <td>0.040913</td>
      <td>0.039222</td>
      <td>-0.083546</td>
      <td>-0.008740</td>
      <td>0.142779</td>
      <td>0.253684</td>
      <td>0.250495</td>
    </tr>
    <tr>
      <th>mnth</th>
      <td>0.489164</td>
      <td>0.830386</td>
      <td>-0.010473</td>
      <td>1.000000</td>
      <td>-0.005772</td>
      <td>0.018430</td>
      <td>0.010400</td>
      <td>-0.003477</td>
      <td>0.005400</td>
      <td>0.201691</td>
      <td>0.208096</td>
      <td>0.164411</td>
      <td>-0.135386</td>
      <td>0.068457</td>
      <td>0.122273</td>
      <td>0.120638</td>
    </tr>
    <tr>
      <th>hr</th>
      <td>-0.004775</td>
      <td>-0.006117</td>
      <td>-0.003867</td>
      <td>-0.005772</td>
      <td>1.000000</td>
      <td>0.000479</td>
      <td>-0.003498</td>
      <td>0.002285</td>
      <td>-0.020203</td>
      <td>0.137603</td>
      <td>0.133750</td>
      <td>-0.276498</td>
      <td>0.137252</td>
      <td>0.301202</td>
      <td>0.374141</td>
      <td>0.394071</td>
    </tr>
    <tr>
      <th>holiday</th>
      <td>0.014723</td>
      <td>-0.009585</td>
      <td>0.006692</td>
      <td>0.018430</td>
      <td>0.000479</td>
      <td>1.000000</td>
      <td>-0.102088</td>
      <td>-0.252471</td>
      <td>-0.017036</td>
      <td>-0.027340</td>
      <td>-0.030973</td>
      <td>-0.010588</td>
      <td>0.003988</td>
      <td>0.031564</td>
      <td>-0.047345</td>
      <td>-0.030927</td>
    </tr>
    <tr>
      <th>weekday</th>
      <td>0.001357</td>
      <td>-0.002335</td>
      <td>-0.004485</td>
      <td>0.010400</td>
      <td>-0.003498</td>
      <td>-0.102088</td>
      <td>1.000000</td>
      <td>0.035955</td>
      <td>0.003311</td>
      <td>-0.001795</td>
      <td>-0.008821</td>
      <td>-0.037158</td>
      <td>0.011502</td>
      <td>0.032721</td>
      <td>0.021578</td>
      <td>0.026900</td>
    </tr>
    <tr>
      <th>workingday</th>
      <td>-0.003416</td>
      <td>0.013743</td>
      <td>-0.002196</td>
      <td>-0.003477</td>
      <td>0.002285</td>
      <td>-0.252471</td>
      <td>0.035955</td>
      <td>1.000000</td>
      <td>0.044672</td>
      <td>0.055390</td>
      <td>0.054667</td>
      <td>0.015688</td>
      <td>-0.011830</td>
      <td>-0.300942</td>
      <td>0.134326</td>
      <td>0.030284</td>
    </tr>
    <tr>
      <th>weathersit</th>
      <td>-0.014198</td>
      <td>-0.014524</td>
      <td>-0.019157</td>
      <td>0.005400</td>
      <td>-0.020203</td>
      <td>-0.017036</td>
      <td>0.003311</td>
      <td>0.044672</td>
      <td>1.000000</td>
      <td>-0.102640</td>
      <td>-0.105563</td>
      <td>0.418130</td>
      <td>0.026226</td>
      <td>-0.152628</td>
      <td>-0.120966</td>
      <td>-0.142426</td>
    </tr>
    <tr>
      <th>temp</th>
      <td>0.136178</td>
      <td>0.312025</td>
      <td>0.040913</td>
      <td>0.201691</td>
      <td>0.137603</td>
      <td>-0.027340</td>
      <td>-0.001795</td>
      <td>0.055390</td>
      <td>-0.102640</td>
      <td>1.000000</td>
      <td>0.987672</td>
      <td>-0.069881</td>
      <td>-0.023125</td>
      <td>0.459616</td>
      <td>0.335361</td>
      <td>0.404772</td>
    </tr>
    <tr>
      <th>atemp</th>
      <td>0.137615</td>
      <td>0.319380</td>
      <td>0.039222</td>
      <td>0.208096</td>
      <td>0.133750</td>
      <td>-0.030973</td>
      <td>-0.008821</td>
      <td>0.054667</td>
      <td>-0.105563</td>
      <td>0.987672</td>
      <td>1.000000</td>
      <td>-0.051918</td>
      <td>-0.062336</td>
      <td>0.454080</td>
      <td>0.332559</td>
      <td>0.400929</td>
    </tr>
    <tr>
      <th>hum</th>
      <td>0.009577</td>
      <td>0.150625</td>
      <td>-0.083546</td>
      <td>0.164411</td>
      <td>-0.276498</td>
      <td>-0.010588</td>
      <td>-0.037158</td>
      <td>0.015688</td>
      <td>0.418130</td>
      <td>-0.069881</td>
      <td>-0.051918</td>
      <td>1.000000</td>
      <td>-0.290105</td>
      <td>-0.347028</td>
      <td>-0.273933</td>
      <td>-0.322911</td>
    </tr>
    <tr>
      <th>windspeed</th>
      <td>-0.074505</td>
      <td>-0.149773</td>
      <td>-0.008740</td>
      <td>-0.135386</td>
      <td>0.137252</td>
      <td>0.003988</td>
      <td>0.011502</td>
      <td>-0.011830</td>
      <td>0.026226</td>
      <td>-0.023125</td>
      <td>-0.062336</td>
      <td>-0.290105</td>
      <td>1.000000</td>
      <td>0.090287</td>
      <td>0.082321</td>
      <td>0.093234</td>
    </tr>
    <tr>
      <th>casual</th>
      <td>0.158295</td>
      <td>0.120206</td>
      <td>0.142779</td>
      <td>0.068457</td>
      <td>0.301202</td>
      <td>0.031564</td>
      <td>0.032721</td>
      <td>-0.300942</td>
      <td>-0.152628</td>
      <td>0.459616</td>
      <td>0.454080</td>
      <td>-0.347028</td>
      <td>0.090287</td>
      <td>1.000000</td>
      <td>0.506618</td>
      <td>0.694564</td>
    </tr>
    <tr>
      <th>registered</th>
      <td>0.282046</td>
      <td>0.174226</td>
      <td>0.253684</td>
      <td>0.122273</td>
      <td>0.374141</td>
      <td>-0.047345</td>
      <td>0.021578</td>
      <td>0.134326</td>
      <td>-0.120966</td>
      <td>0.335361</td>
      <td>0.332559</td>
      <td>-0.273933</td>
      <td>0.082321</td>
      <td>0.506618</td>
      <td>1.000000</td>
      <td>0.972151</td>
    </tr>
    <tr>
      <th>cnt</th>
      <td>0.278379</td>
      <td>0.178056</td>
      <td>0.250495</td>
      <td>0.120638</td>
      <td>0.394071</td>
      <td>-0.030927</td>
      <td>0.026900</td>
      <td>0.030284</td>
      <td>-0.142426</td>
      <td>0.404772</td>
      <td>0.400929</td>
      <td>-0.322911</td>
      <td>0.093234</td>
      <td>0.694564</td>
      <td>0.972151</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



# Calculating Features

- We are going to introduce some order in hour data by separating the hours in terms of morning, afternoon, evening and night


```python
def assign_label(hour):
    if (hour > 6 ) & (hour <= 12):
        return 1
    if (hour > 12 ) & (hour <= 18):
        return 2
    if (hour > 18 ) & (hour <= 24):
        return 3
    if (hour >= 0 ) & (hour <= 6):
        return 4

bike_rentals['time_label'] = bike_rentals['hr'].apply(lambda x: assign_label(x))
```


```python
print(bike_rentals.head())
```

       instant      dteday  season  yr  mnth  hr  holiday  weekday  workingday  \
    0        1  2011-01-01       1   0     1   0        0        6           0   
    1        2  2011-01-01       1   0     1   1        0        6           0   
    2        3  2011-01-01       1   0     1   2        0        6           0   
    3        4  2011-01-01       1   0     1   3        0        6           0   
    4        5  2011-01-01       1   0     1   4        0        6           0   

       weathersit  temp   atemp   hum  windspeed  casual  registered  cnt  \
    0           1  0.24  0.2879  0.81        0.0       3          13   16   
    1           1  0.22  0.2727  0.80        0.0       8          32   40   
    2           1  0.22  0.2727  0.80        0.0       5          27   32   
    3           1  0.24  0.2879  0.75        0.0       3          10   13   
    4           1  0.24  0.2879  0.75        0.0       0           1    1   

       time_label  
    0           4  
    1           4  
    2           4  
    3           4  
    4           4  


# Splitting The Data Into Train And Test Sets

- In this case we are going to use the Mean Squared error, which make sense for our continous data.


```python
how_many_rows = np.int(len(bike_rentals) * .8)

train = bike_rentals.sample(frac=.8)
test = bike_rentals.loc[~bike_rentals.index.isin(train.index)]
```


```python
predictors = list(bike_rentals.columns)

predictors.remove('cnt')
predictors.remove('casual')
predictors.remove('dteday')
predictors.remove('registered')

print(predictors)
```

    ['instant', 'season', 'yr', 'mnth', 'hr', 'holiday', 'weekday', 'workingday', 'weathersit', 'temp', 'atemp', 'hum', 'windspeed', 'time_label']



```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(train[predictors], train['cnt'])

predict = model.predict(test[predictors])

mse = np.mean((test['cnt'] - predict) ** 2)

print('error: ', mse)

```

    error:  16211.415323715768


- Thought about the error:
    - It is very high, so it should be due to the reason that some data is too high and then there comes this high mean squared.

# Applying Decision Trees

- In order to choose which model fits better our data we are going to checck how decision trees work with this dataframe and after that we will see which one though us a bigger error so we can compare.



```python
from sklearn.tree import DecisionTreeRegressor

model_tree = DecisionTreeRegressor()
model_tree.fit(train[predictors], train['cnt'])
predictions_tree = model_tree.predict(test[predictors])

mse_tree = np.mean((test['cnt'] - predictions_tree) ** 2)

print('mse_tree: ', mse_tree)
```

    mse_tree:  3138.406501726122


- As we can see, using decision tree we are going to get more accuracy in our predictions than with linearregression, because as we proved, the mean squared error is smaller in the dec tree than in Linear regression.

# Applying Random Forest


```python
from sklearn.ensemble import RandomForestRegressor

model_forest = RandomForestRegressor()
model_forest.fit(train[predictors], train['cnt'])
predict_forest = model_forest.predict(test[predictors])

mse_forest = np.mean((test['cnt'] - predict_forest) ** 2)

print('mse_forest: ', mse_forest)

```

    mse_forest:  1906.2452301495964



```python
Github link:
`https://github.com/coderHook/Project---Predicting-Bike-Rentals-using-Forest-Decision-Model`
```
