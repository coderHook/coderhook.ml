+++
# Date this page was created.
date = "2017-07-27"

# Project title.
title = "Exploring the tendencies in Celebrating Thanksgiving. "

# Project summary to display on homepage.
summary = "In this project we are going to explore the tendencies that people follow in this celebration. We will correlate people that celebrate it, travelling distance and income."

# Optional image to display on homepage (relative to `static/img/headers` folder).
image_preview = "thanksgiving.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["datascience"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "thanksgiving.jpg"
caption = ""

+++



# Exploring the tendencies in Celebrating Thanksgiving.



   ### In this project we are going to explore the tendencies that people follow in this celebration.

   #### First, we are going to check what dishes and desserts are the favourites among people.
   #### Secondly, we are going to get the income and see how it is correlated from How far people travel to celebrate Thnksgiving.
   #### Finally, we are going to conclude our project Linking celebration and friends and observing what age range tends to celebrate most Thanksgiving.







```python


import pandas as pd

dataset = pd.read_csv('https://raw.githubusercontent.com/fivethirtyeight/data/master/thanksgiving-2015/thanksgiving-2015-poll-data.csv', encoding='latin1')
dataset.head(5)
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
      <th>RespondentID</th>
      <th>Do you celebrate Thanksgiving?</th>
      <th>What is typically the main dish at your Thanksgiving dinner?</th>
      <th>What is typically the main dish at your Thanksgiving dinner? - Other (please specify)</th>
      <th>How is the main dish typically cooked?</th>
      <th>How is the main dish typically cooked? - Other (please specify)</th>
      <th>What kind of stuffing/dressing do you typically have?</th>
      <th>What kind of stuffing/dressing do you typically have? - Other (please specify)</th>
      <th>What type of cranberry saucedo you typically have?</th>
      <th>What type of cranberry saucedo you typically have? - Other (please specify)</th>
      <th>...</th>
      <th>Have you ever tried to meet up with hometown friends on Thanksgiving night?</th>
      <th>Have you ever attended a "Friendsgiving?"</th>
      <th>Will you shop any Black Friday sales on Thanksgiving Day?</th>
      <th>Do you work in retail?</th>
      <th>Will you employer make you work on Black Friday?</th>
      <th>How would you describe where you live?</th>
      <th>Age</th>
      <th>What is your gender?</th>
      <th>How much total combined money did all members of your HOUSEHOLD earn last year?</th>
      <th>US Region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4337954960</td>
      <td>Yes</td>
      <td>Turkey</td>
      <td>NaN</td>
      <td>Baked</td>
      <td>NaN</td>
      <td>Bread-based</td>
      <td>NaN</td>
      <td>None</td>
      <td>NaN</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Suburban</td>
      <td>18 - 29</td>
      <td>Male</td>
      <td>$75,000 to $99,999</td>
      <td>Middle Atlantic</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4337951949</td>
      <td>Yes</td>
      <td>Turkey</td>
      <td>NaN</td>
      <td>Baked</td>
      <td>NaN</td>
      <td>Bread-based</td>
      <td>NaN</td>
      <td>Other (please specify)</td>
      <td>Homemade cranberry gelatin ring</td>
      <td>...</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>Rural</td>
      <td>18 - 29</td>
      <td>Female</td>
      <td>$50,000 to $74,999</td>
      <td>East South Central</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4337935621</td>
      <td>Yes</td>
      <td>Turkey</td>
      <td>NaN</td>
      <td>Roasted</td>
      <td>NaN</td>
      <td>Rice-based</td>
      <td>NaN</td>
      <td>Homemade</td>
      <td>NaN</td>
      <td>...</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>Suburban</td>
      <td>18 - 29</td>
      <td>Male</td>
      <td>$0 to $9,999</td>
      <td>Mountain</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4337933040</td>
      <td>Yes</td>
      <td>Turkey</td>
      <td>NaN</td>
      <td>Baked</td>
      <td>NaN</td>
      <td>Bread-based</td>
      <td>NaN</td>
      <td>Homemade</td>
      <td>NaN</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Urban</td>
      <td>30 - 44</td>
      <td>Male</td>
      <td>$200,000 and up</td>
      <td>Pacific</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4337931983</td>
      <td>Yes</td>
      <td>Tofurkey</td>
      <td>NaN</td>
      <td>Baked</td>
      <td>NaN</td>
      <td>Bread-based</td>
      <td>NaN</td>
      <td>Canned</td>
      <td>NaN</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Urban</td>
      <td>30 - 44</td>
      <td>Male</td>
      <td>$100,000 to $124,999</td>
      <td>Pacific</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 65 columns</p>
</div>




```python
header = dataset.columns.unique()

```


```python
cel_thanks_count = dataset["Do you celebrate Thanksgiving?"].value_counts()
cel_thanks = dataset[dataset["Do you celebrate Thanksgiving?"] == 'Yes']

cel_thanks.head()
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
      <th>RespondentID</th>
      <th>Do you celebrate Thanksgiving?</th>
      <th>What is typically the main dish at your Thanksgiving dinner?</th>
      <th>What is typically the main dish at your Thanksgiving dinner? - Other (please specify)</th>
      <th>How is the main dish typically cooked?</th>
      <th>How is the main dish typically cooked? - Other (please specify)</th>
      <th>What kind of stuffing/dressing do you typically have?</th>
      <th>What kind of stuffing/dressing do you typically have? - Other (please specify)</th>
      <th>What type of cranberry saucedo you typically have?</th>
      <th>What type of cranberry saucedo you typically have? - Other (please specify)</th>
      <th>...</th>
      <th>Have you ever tried to meet up with hometown friends on Thanksgiving night?</th>
      <th>Have you ever attended a "Friendsgiving?"</th>
      <th>Will you shop any Black Friday sales on Thanksgiving Day?</th>
      <th>Do you work in retail?</th>
      <th>Will you employer make you work on Black Friday?</th>
      <th>How would you describe where you live?</th>
      <th>Age</th>
      <th>What is your gender?</th>
      <th>How much total combined money did all members of your HOUSEHOLD earn last year?</th>
      <th>US Region</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4337954960</td>
      <td>Yes</td>
      <td>Turkey</td>
      <td>NaN</td>
      <td>Baked</td>
      <td>NaN</td>
      <td>Bread-based</td>
      <td>NaN</td>
      <td>None</td>
      <td>NaN</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Suburban</td>
      <td>18 - 29</td>
      <td>Male</td>
      <td>$75,000 to $99,999</td>
      <td>Middle Atlantic</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4337951949</td>
      <td>Yes</td>
      <td>Turkey</td>
      <td>NaN</td>
      <td>Baked</td>
      <td>NaN</td>
      <td>Bread-based</td>
      <td>NaN</td>
      <td>Other (please specify)</td>
      <td>Homemade cranberry gelatin ring</td>
      <td>...</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>Rural</td>
      <td>18 - 29</td>
      <td>Female</td>
      <td>$50,000 to $74,999</td>
      <td>East South Central</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4337935621</td>
      <td>Yes</td>
      <td>Turkey</td>
      <td>NaN</td>
      <td>Roasted</td>
      <td>NaN</td>
      <td>Rice-based</td>
      <td>NaN</td>
      <td>Homemade</td>
      <td>NaN</td>
      <td>...</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>No</td>
      <td>NaN</td>
      <td>Suburban</td>
      <td>18 - 29</td>
      <td>Male</td>
      <td>$0 to $9,999</td>
      <td>Mountain</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4337933040</td>
      <td>Yes</td>
      <td>Turkey</td>
      <td>NaN</td>
      <td>Baked</td>
      <td>NaN</td>
      <td>Bread-based</td>
      <td>NaN</td>
      <td>Homemade</td>
      <td>NaN</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Urban</td>
      <td>30 - 44</td>
      <td>Male</td>
      <td>$200,000 and up</td>
      <td>Pacific</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4337931983</td>
      <td>Yes</td>
      <td>Tofurkey</td>
      <td>NaN</td>
      <td>Baked</td>
      <td>NaN</td>
      <td>Bread-based</td>
      <td>NaN</td>
      <td>Canned</td>
      <td>NaN</td>
      <td>...</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>NaN</td>
      <td>Urban</td>
      <td>30 - 44</td>
      <td>Male</td>
      <td>$100,000 to $124,999</td>
      <td>Pacific</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 65 columns</p>
</div>



### 2) Exploring Main dishes people tend to eat during Thanksgiving dinner


```python
thanks_dishes_count = dataset['What is typically the main dish at your Thanksgiving dinner?'].value_counts()
print('         Main Dish \n', thanks_dishes_count)

tofurkey_dish = dataset[dataset['What is typically the main dish at your Thanksgiving dinner?'] == 'Tofurkey']
tofurkey_have_gravy = tofurkey_dish['Do you typically have gravy?']
print(tofurkey_have_gravy)
```

             Main Dish
     Turkey                    859
    Other (please specify)     35
    Ham/Pork                   29
    Tofurkey                   20
    Chicken                    12
    Roast beef                 11
    I don't know                5
    Turducken                   3
    Name: What is typically the main dish at your Thanksgiving dinner?, dtype: int64
    4      Yes
    33     Yes
    69      No
    72      No
    77     Yes
    145    Yes
    175    Yes
    218     No
    243    Yes
    275     No
    393    Yes
    399    Yes
    571    Yes
    594    Yes
    628     No
    774     No
    820     No
    837    Yes
    860     No
    953    Yes
    Name: Do you typically have gravy?, dtype: object


###### Results:
- 20 have Tofurkey for dinner
- From those, 12 use gravy on it.

### 3) Let's see what pies people eat



```python
apple_isnull = pd.isnull(dataset['Which type of pie is typically served at your Thanksgiving dinner? Please select all that apply. - Apple'])
pumpkin_isnull = pd.isnull(dataset['Which type of pie is typically served at your Thanksgiving dinner? Please select all that apply. - Pumpkin'])
pecan_isnull = pd.isnull(dataset['Which type of pie is typically served at your Thanksgiving dinner? Please select all that apply. - Pecan'])

ate_pies = apple_isnull & pumpkin_isnull & pecan_isnull
print(ate_pies.value_counts())

```

    False    876
    True     182
    dtype: int64


### 4) Converting Age to Numeric


```python
def ext_age(age):
    if pd.isnull(age):
        return None

    age_split = age.split(' ')
    age_splited = age_split[0].replace('+', '')
    return int(age_splited)

example = ext_age(dataset['Age'][14])  

dataset['int_age'] = dataset['Age'].apply(ext_age)

dataset['int_age'].describe()
```




    count    1025.000000
    mean       39.383415
    std        15.398493
    min        18.000000
    25%        30.000000
    50%        45.000000
    75%        60.000000
    max        60.000000
    Name: int_age, dtype: float64



###### Results:
- As we can observe, with the describe method we have some measurements on the ages we are working with.
- We have to be aware that the ages are not exact, because our original data contains a range and we are taking the lowest age in that range. Not true ages but quitte accurate according to the data we are working with.


```python
dataset['Age'].value_counts()
```




    45 - 59    286
    60+        264
    30 - 44    259
    18 - 29    216
    Name: Age, dtype: int64



### 5) Converting Income to Numeric


```python
dataset['How much total combined money did all members of your HOUSEHOLD earn last year?'].value_counts()

#Function to convert income_string to a data value.
def ext_income(income):
    if pd.isnull(income):
        return None

    income_split = income.split(' ')
    if income_split[0] == 'Prefer':
        return None
    income_splitted = income_split[0].replace("$", "").replace(",", "")

    return int(income_splitted)

example1 = dataset['How much total combined money did all members of your HOUSEHOLD earn last year?'][0].split(' ')

dataset['int_income']  = dataset['How much total combined money did all members of your HOUSEHOLD earn last year?'].apply(ext_income)
dataset['int_income'].describe()
```




    count       889.000000
    mean      74077.615298
    std       59360.742902
    min           0.000000
    25%       25000.000000
    50%       50000.000000
    75%      100000.000000
    max      200000.000000
    Name: int_income, dtype: float64



###### Results:
WE should be aware that we have a range of salary but we are only using the lowest value in each range.

We can se that the mean salary is pretty high. We have also a large standard deviation.


### 6) Correlating Travel Distance and Income


```python
dataset['How far will you travel for Thanksgiving?'].value_counts()
```




    Thanksgiving is happening at my home--I won't travel at all                         396
    Thanksgiving is local--it will take place in the town I live in                     276
    Thanksgiving is out of town but not too far--it's a drive of a few hours or less    197
    Thanksgiving is out of town and far away--I have to drive several hours or fly       82
    Name: How far will you travel for Thanksgiving?, dtype: int64




```python
dataset['How far will you travel for Thanksgiving?'][dataset['int_income'] < 150000].value_counts()
```




    Thanksgiving is happening at my home--I won't travel at all                         281
    Thanksgiving is local--it will take place in the town I live in                     203
    Thanksgiving is out of town but not too far--it's a drive of a few hours or less    150
    Thanksgiving is out of town and far away--I have to drive several hours or fly       55
    Name: How far will you travel for Thanksgiving?, dtype: int64




```python
dataset['How far will you travel for Thanksgiving?'][dataset['int_income'] > 150000].value_counts()
```




    Thanksgiving is happening at my home--I won't travel at all                         49
    Thanksgiving is local--it will take place in the town I live in                     25
    Thanksgiving is out of town but not too far--it's a drive of a few hours or less    16
    Thanksgiving is out of town and far away--I have to drive several hours or fly      12
    Name: How far will you travel for Thanksgiving?, dtype: int64



#### Results:
- People with incomes lower than 150000 is more used to celebrate thankgiing at home and less used to go out of town and far away.

- People with high incomes (>150000) Celebrates it at home as well.

- One interesting data is that people with income lower than 150000 is more used to go out of town but not far away than people with high income, it can be because most of them live out of their family town and they have to move to visit them.

## 7) Linking Friendship and Age


```python
dataset.pivot_table(
    index = 'Have you ever tried to meet up with hometown friends on Thanksgiving night?',
    columns = 'Have you ever attended a "Friendsgiving?"',
    values = 'int_age'
)
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
      <th>Have you ever attended a "Friendsgiving?"</th>
      <th>No</th>
      <th>Yes</th>
    </tr>
    <tr>
      <th>Have you ever tried to meet up with hometown friends on Thanksgiving night?</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>No</th>
      <td>42.283702</td>
      <td>37.010526</td>
    </tr>
    <tr>
      <th>Yes</th>
      <td>41.475410</td>
      <td>33.976744</td>
    </tr>
  </tbody>
</table>
</div>




```python
dataset.pivot_table(
    index = 'Have you ever tried to meet up with hometown friends on Thanksgiving night?',
    columns = 'Have you ever attended a "Friendsgiving?"',
    values = 'int_income'
)
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
      <th>Have you ever attended a "Friendsgiving?"</th>
      <th>No</th>
      <th>Yes</th>
    </tr>
    <tr>
      <th>Have you ever tried to meet up with hometown friends on Thanksgiving night?</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>No</th>
      <td>78914.549654</td>
      <td>72894.736842</td>
    </tr>
    <tr>
      <th>Yes</th>
      <td>78750.000000</td>
      <td>66019.736842</td>
    </tr>
  </tbody>
</table>
</div>



#### Findings:
- As we can appreciate, Young people is more likely to celebrate thanksgiving than olders.


```python

```
