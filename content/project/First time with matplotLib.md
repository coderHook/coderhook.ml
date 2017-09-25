+++
# Date this page was created.
date = "2017-07-26"

# Project title.
title = " Using Matplotlib, first steps. "

# Project summary to display on homepage.
summary = "Introducing ourself in the matplotlib art, generating bar charts, scatter plots and linear Plots."

# Optional image to display on homepage (relative to `static/img/headers` folder).
image_preview = "matplotlib.png"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["datascience"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "matplotlib.png"
caption = ""

+++



# First Time with Matplotlib.

### An easy way to visualize data using the main tools availables.

In this notebook we are going to show 3 kind of plots:
    - Linear Plots: Gave a good sense on the tendency of the data.
    - Scatter Plot: Great to see if the data follow a tendency or if it is too "scatter".
    - Bar Plots: Easy to compare data an see which of the variables appears more frequently or even the distribution of it.

##### After it, we will extract some insight that will help us for following researchs.



```python
%matplotlib inline

import matplotlib.pyplot as plt
import pandas as pd

unrate = pd.read_csv("unrate.csv")
unrate['DATE'] = pd.to_datetime(unrate['DATE']) #pd.to_datetime() transforms date string into a date format.

plt.plot(unrate['DATE'][0:12], unrate['VALUE'][:12])
plt.xticks(rotation = 90)
plt.xlabel("Month")
plt.ylabel("Unemployment Rate")
plt.title("Monthly Unemployment Trends, 1948")
plt.show()
```


![png](/img/ds/matplotlib/output_1_0.png)



```python
fig = plt.figure(figsize=(10,6))
colors = ['red', 'blue', 'green', 'orange', 'black']
labels = ['1948', '1949', '1950', '1951', '1952']
unrate['MONTH'] = unrate['DATE'].dt.month

for i in range(5):
    start_index = i*12
    end_index = (i+1)*12
    subset = unrate[start_index:end_index]
    label = str(1948 + i)
    plt.plot(subset['MONTH'], subset['VALUE'], c=colors[i], label=labels[i])
plt.title("Monthly Unemployment Trends, 1948-1952")
plt.xlabel("Month, Integer")
plt.ylabel("Unemployment Rate, Percent")
plt.legend(loc='upper left')

plt.show()
```


![png](/img/ds/matplotlib/output_2_0.png)


# Scatter Plot & Bar Plot


```python
import seaborn as sns

df = pd.read_csv("fandango_score_comparison.csv")

columns = ['FILM', 'RT_user_norm', 'Metacritic_user_nom', 'IMDB_norm', 'Fandango_Ratingvalue', 'Fandango_Stars', 'Metacritic_norm_round']

df = review[columns]

df.head()
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
      <th>FILM</th>
      <th>RT_user_norm</th>
      <th>Metacritic_user_nom</th>
      <th>IMDB_norm</th>
      <th>Fandango_Ratingvalue</th>
      <th>Fandango_Stars</th>
      <th>Metacritic_norm_round</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Avengers: Age of Ultron (2015)</td>
      <td>4.3</td>
      <td>3.55</td>
      <td>3.90</td>
      <td>4.5</td>
      <td>5.0</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cinderella (2015)</td>
      <td>4.0</td>
      <td>3.75</td>
      <td>3.55</td>
      <td>4.5</td>
      <td>5.0</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ant-Man (2015)</td>
      <td>4.5</td>
      <td>4.05</td>
      <td>3.90</td>
      <td>4.5</td>
      <td>5.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Do You Believe? (2015)</td>
      <td>4.2</td>
      <td>2.35</td>
      <td>2.70</td>
      <td>4.5</td>
      <td>5.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hot Tub Time Machine 2 (2015)</td>
      <td>1.4</td>
      <td>1.70</td>
      <td>2.55</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>1.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.scatter(df['Metacritic_norm_round'], df['Fandango_Stars'])
sns.plt.show()
```


![png](/img/ds/matplotlib/output_5_0.png)


### Bar Plot
 - Bar plot are really useful to compare data between some variables, in this case we can compare easily for instance, each of the columns with the frecuency.


```python
df['Metacritic_norm_round'].plot(kind="hist")
df['Fandango_Stars'].plot(kind="hist")
plt.legend()
sns.plt.show()
```


![png](/img/ds/matplotlib/output_7_0.png)


- In this case we can see somethign really interesting, Fandango_Stars doesnt have valuation less than 3 which is suspicious, and should result in more things to look for on the data to see what is happening there.

# Conclusion

Is it super easy to compare data using matplotlib, we also learnt that seaborn can gave us other sense on the visualization and make this more understandable and finally, we practice the 3 kind of plots, inear plots, Scatter plot and Bar plot.


```python

```
