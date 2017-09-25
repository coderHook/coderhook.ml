+++
# Date this page was created.
date = "2017-04-27"

# Project title.
title = "Predicting Board Games Reviews, Custers, Correlations and choosing an Error. "

# Project summary to display on homepage.
summary = "In this project we are going to first, see how to pick a metric error for our model, we are going to work with clusters and check for correlations, and finally we will create a model for our predictions. "

# Optional image to display on homepage (relative to `static/img/headers` folder).
image_preview = "boardgames.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["datascience"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "headers/boardgames.jpg"
caption = "Which ones get the highest reviews?"

+++




# Predicting Board Games Reviews

### In this project we are going to first, see how to pick a metric error for our model, we are going to work with clusters and check for correlations, and finally we will create a model for our predictions.


```python
import pandas as pd
import csv

board_games = pd.read_csv("board_games.csv")
board_games.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>type</th>
      <th>name</th>
      <th>yearpublished</th>
      <th>minplayers</th>
      <th>maxplayers</th>
      <th>playingtime</th>
      <th>minplaytime</th>
      <th>maxplaytime</th>
      <th>minage</th>
      <th>users_rated</th>
      <th>average_rating</th>
      <th>bayes_average_rating</th>
      <th>total_owners</th>
      <th>total_traders</th>
      <th>total_wanters</th>
      <th>total_wishers</th>
      <th>total_comments</th>
      <th>total_weights</th>
      <th>average_weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>12333</td>
      <td>boardgame</td>
      <td>Twilight Struggle</td>
      <td>2005.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>180.0</td>
      <td>180.0</td>
      <td>180.0</td>
      <td>13.0</td>
      <td>20113</td>
      <td>8.33774</td>
      <td>8.22186</td>
      <td>26647</td>
      <td>372</td>
      <td>1219</td>
      <td>5865</td>
      <td>5347</td>
      <td>2562</td>
      <td>3.4785</td>
    </tr>
    <tr>
      <th>1</th>
      <td>120677</td>
      <td>boardgame</td>
      <td>Terra Mystica</td>
      <td>2012.0</td>
      <td>2.0</td>
      <td>5.0</td>
      <td>150.0</td>
      <td>60.0</td>
      <td>150.0</td>
      <td>12.0</td>
      <td>14383</td>
      <td>8.28798</td>
      <td>8.14232</td>
      <td>16519</td>
      <td>132</td>
      <td>1586</td>
      <td>6277</td>
      <td>2526</td>
      <td>1423</td>
      <td>3.8939</td>
    </tr>
    <tr>
      <th>2</th>
      <td>102794</td>
      <td>boardgame</td>
      <td>Caverna: The Cave Farmers</td>
      <td>2013.0</td>
      <td>1.0</td>
      <td>7.0</td>
      <td>210.0</td>
      <td>30.0</td>
      <td>210.0</td>
      <td>12.0</td>
      <td>9262</td>
      <td>8.28994</td>
      <td>8.06886</td>
      <td>12230</td>
      <td>99</td>
      <td>1476</td>
      <td>5600</td>
      <td>1700</td>
      <td>777</td>
      <td>3.7761</td>
    </tr>
    <tr>
      <th>3</th>
      <td>25613</td>
      <td>boardgame</td>
      <td>Through the Ages: A Story of Civilization</td>
      <td>2006.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>240.0</td>
      <td>240.0</td>
      <td>240.0</td>
      <td>12.0</td>
      <td>13294</td>
      <td>8.20407</td>
      <td>8.05804</td>
      <td>14343</td>
      <td>362</td>
      <td>1084</td>
      <td>5075</td>
      <td>3378</td>
      <td>1642</td>
      <td>4.1590</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3076</td>
      <td>boardgame</td>
      <td>Puerto Rico</td>
      <td>2002.0</td>
      <td>2.0</td>
      <td>5.0</td>
      <td>150.0</td>
      <td>90.0</td>
      <td>150.0</td>
      <td>12.0</td>
      <td>39883</td>
      <td>8.14261</td>
      <td>8.04524</td>
      <td>44362</td>
      <td>795</td>
      <td>861</td>
      <td>5414</td>
      <td>9173</td>
      <td>5213</td>
      <td>3.2943</td>
    </tr>
  </tbody>
</table>
</div>




```python
board_games.shape
```




    (81312, 20)




```python
board_games = board_games.dropna(axis=0)
```


```python
board_games.shape
```




    (81268, 20)




```python
board_games = board_games[board_games['users_rated'] > 0]
```


```python
board_games.shape
```




    (56894, 20)



 # Picking An Error Metric



```python
import matplotlib.pyplot as plt
%matplotlib inline

plt.hist(board_games['average_rating'])
plt.show()
```


![png](/img/ds/board_review/output_8_0.png)



```python
plt.boxplot(board_games['average_rating'])
plt.show()
```


![png](/img/ds/board_review/output_9_0.png)



```python
print(board_games['average_rating'].std())
print(board_games['average_rating'].mean())
```

    1.57882993483
    6.01611284933


- AS the data is continous using mean square error makes sense.

- But it is not the only possibility, as it is a linear regression and we want to meassure the distance between the actual value and the predicted one, we can also use, mean square and mean median errors.

- DEFINETLY NOT to use AUC or any other classification error metric cause this is not the case we are going to work in.

# Plotting Clusters


```python
from sklearn.cluster import KMeans
import numpy as np

kmeans = KMeans(n_clusters = 5)

numeric_columns = board_games.iloc[:, 3:]
numeric_columns.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>yearpublished</th>
      <th>minplayers</th>
      <th>maxplayers</th>
      <th>playingtime</th>
      <th>minplaytime</th>
      <th>maxplaytime</th>
      <th>minage</th>
      <th>users_rated</th>
      <th>average_rating</th>
      <th>bayes_average_rating</th>
      <th>total_owners</th>
      <th>total_traders</th>
      <th>total_wanters</th>
      <th>total_wishers</th>
      <th>total_comments</th>
      <th>total_weights</th>
      <th>average_weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2005.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>180.0</td>
      <td>180.0</td>
      <td>180.0</td>
      <td>13.0</td>
      <td>20113</td>
      <td>8.33774</td>
      <td>8.22186</td>
      <td>26647</td>
      <td>372</td>
      <td>1219</td>
      <td>5865</td>
      <td>5347</td>
      <td>2562</td>
      <td>3.4785</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2012.0</td>
      <td>2.0</td>
      <td>5.0</td>
      <td>150.0</td>
      <td>60.0</td>
      <td>150.0</td>
      <td>12.0</td>
      <td>14383</td>
      <td>8.28798</td>
      <td>8.14232</td>
      <td>16519</td>
      <td>132</td>
      <td>1586</td>
      <td>6277</td>
      <td>2526</td>
      <td>1423</td>
      <td>3.8939</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013.0</td>
      <td>1.0</td>
      <td>7.0</td>
      <td>210.0</td>
      <td>30.0</td>
      <td>210.0</td>
      <td>12.0</td>
      <td>9262</td>
      <td>8.28994</td>
      <td>8.06886</td>
      <td>12230</td>
      <td>99</td>
      <td>1476</td>
      <td>5600</td>
      <td>1700</td>
      <td>777</td>
      <td>3.7761</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2006.0</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>240.0</td>
      <td>240.0</td>
      <td>240.0</td>
      <td>12.0</td>
      <td>13294</td>
      <td>8.20407</td>
      <td>8.05804</td>
      <td>14343</td>
      <td>362</td>
      <td>1084</td>
      <td>5075</td>
      <td>3378</td>
      <td>1642</td>
      <td>4.1590</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2002.0</td>
      <td>2.0</td>
      <td>5.0</td>
      <td>150.0</td>
      <td>90.0</td>
      <td>150.0</td>
      <td>12.0</td>
      <td>39883</td>
      <td>8.14261</td>
      <td>8.04524</td>
      <td>44362</td>
      <td>795</td>
      <td>861</td>
      <td>5414</td>
      <td>9173</td>
      <td>5213</td>
      <td>3.2943</td>
    </tr>
  </tbody>
</table>
</div>




```python
kmeans.fit(numeric_columns)
```




    KMeans(copy_x=True, init='k-means++', max_iter=300, n_clusters=5, n_init=10,
        n_jobs=1, precompute_distances='auto', random_state=None, tol=0.0001,
        verbose=0)




```python
labels = kmeans.labels_
print(labels)
```

    [1 1 1 ..., 0 0 0]



```python
game_mean = numeric_columns.apply(np.mean, axis = 1)
game_mean.head()
```




    0    3806.296359
    1    2662.195541
    2    1979.243229
    3    2467.201242
    4    6360.675421
    dtype: float64




```python
game_std = numeric_columns.apply(np.std, axis = 1)

plt.scatter(x=game_mean, y=game_std, c=game_std)
plt.show()
```


![png](/img/ds/board_review/output_17_0.png)


### Results:
    - We can see that there are few games that are played by a lot of players. Most games dont get played that much but a few get plaed by a lot of players.

# Finding Correlations


```python
correlations = numeric_columns.corr()

correlations['average_rating']
```




    yearpublished           0.108461
    minplayers             -0.032701
    maxplayers             -0.008335
    playingtime             0.048994
    minplaytime             0.043985
    maxplaytime             0.048994
    minage                  0.210049
    users_rated             0.112564
    average_rating          1.000000
    bayes_average_rating    0.231563
    total_owners            0.137478
    total_traders           0.119452
    total_wanters           0.196566
    total_wishers           0.171375
    total_comments          0.123714
    total_weights           0.109691
    average_weight          0.351081
    Name: average_rating, dtype: float64



- We can see that average_weight is highly correlated with average_rating, also, yearspublished has a good correlation which indicates that new games get better ratings. Another example is minage, as it is bigger has more rating.


```python
cols_dont_corr = list(numeric_columns.columns)
cols_dont_corr.remove('bayes_average_rating')
cols_dont_corr.remove('average_rating')
# This columns are eliminated because seems that they do not correlate with average_rating

corr_cols = cols_dont_corr

```

# Creating A Model

- Lets create a linear regression model and make some predictions about the  data.


```python
from sklearn.linear_model import LinearRegression

lr = LinearRegression()
lr.fit(board_games[corr_cols], board_games['average_rating'])
predictions = lr.predict(board_games[corr_cols])

mse = np.mean((predictions - board_games['average_rating']) ** 2)
```


```python
print(mse)
```

    2.09339697583


- Our ERROR here is very close to the standard deviation, which means that our model does not predict well.
