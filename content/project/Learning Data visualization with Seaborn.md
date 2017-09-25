+++
# Date this page was created.
date = "2017-07-27"

# Project title.
title = "Learning Data Visualization with Seaborn and Python. "

# Project summary to display on homepage.
summary = "In this project, we are going to present some samples on how to use seaborn to get a better visualization."

# Optional image to display on homepage (relative to `static/img/headers` folder).
image_preview = "seaborn.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["datascience"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "seaborn.jpg"
caption = ""

+++



# Learning Data Visualization with Seaborn and Python.

### In this project, we are going to present some samples on how to use seaborn to get a better visualization.

    - We are going to cover:
        - Creating an Histogram.
        - Generating a Density Plot.
        - Modifying the Appearence of the plots.
        - Conditional Distributions Using A Single Condition.
        - Creating Conditional Plots Using Two Conditions.
        - Creating Conditional Plots Using Three Conditions.
        - Adding a Legend



### Creating an Histogram with Seaborn


```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

titanic = pd.read_csv("train.csv")
cols = ['Survived', 'Pclass', 'Sex', 'Age', 'SibSp', 'Parch', 'Fare', 'Embarked']

titanic = titanic[cols].dropna()

sns.distplot(titanic["Age"])
plt.show()
```

    E:\Anaconda3\lib\site-packages\statsmodels\nonparametric\kdetools.py:20: VisibleDeprecationWarning: using a non-integer number instead of an integer will result in an error in the future
      y = X[:m/2+1] + np.r_[0,X[m/2+1:],0]*1j



![png](/img/ds/seaborn/output_2_1.png)


### Generating A Kernel Density Plot


```python
sns.kdeplot(titanic["Age"], shade="true")
plt.xlabel("Age")
plt.show()
```

    E:\Anaconda3\lib\site-packages\statsmodels\nonparametric\kdetools.py:20: VisibleDeprecationWarning: using a non-integer number instead of an integer will result in an error in the future
      y = X[:m/2+1] + np.r_[0,X[m/2+1:],0]*1j



![png](/img/ds/seaborn/output_4_1.png)


### Modifying The Appearance Of The Plots


```python
sns.set_style("white")
sns.kdeplot(titanic["Age"], shade="true")
sns.despine(left="true", bottom="true")
plt.xlabel("Age")
```

    E:\Anaconda3\lib\site-packages\statsmodels\nonparametric\kdetools.py:20: VisibleDeprecationWarning: using a non-integer number instead of an integer will result in an error in the future
      y = X[:m/2+1] + np.r_[0,X[m/2+1:],0]*1j





    <matplotlib.text.Text at 0x9635cb0>




```python
plt.show()
```


![png](/img/ds/seaborn/output_7_0.png)


### Conditional Distributions Using A Single Condition


```python
g = sns.FacetGrid(titanic, col="Pclass", size = 6)
g.map(sns.kdeplot, "Age", shade="true")
sns.despine(left="true", bottom="true")
plt.show()
```

    E:\Anaconda3\lib\site-packages\statsmodels\nonparametric\kdetools.py:20: VisibleDeprecationWarning: using a non-integer number instead of an integer will result in an error in the future
      y = X[:m/2+1] + np.r_[0,X[m/2+1:],0]*1j



![png](/img/ds/seaborn/output_9_1.png)



![png](/img/ds/seaborn/output_9_2.png)


### Creating Conditional Plots Using Two Conditions


```python
g = sns.FacetGrid(titanic, col="Pclass", row="Survived")
g.map(sns.kdeplot, "Age", shade=True)
sns.despine(left=True, bottom=True)
plt.show()
```

    E:\Anaconda3\lib\site-packages\statsmodels\nonparametric\kdetools.py:20: VisibleDeprecationWarning: using a non-integer number instead of an integer will result in an error in the future
      y = X[:m/2+1] + np.r_[0,X[m/2+1:],0]*1j



![png](/img/ds/seaborn/output_11_1.png)


### Creating Conditional Plots Using Three Conditions


```python
g = sns.FacetGrid(titanic, col="Survived", row="Pclass", hue="Sex")
g.map(sns.kdeplot, "Age", shade=True)
sns.despine(left=True, bottom=True)
plt.show()
```

    E:\Anaconda3\lib\site-packages\statsmodels\nonparametric\kdetools.py:20: VisibleDeprecationWarning: using a non-integer number instead of an integer will result in an error in the future
      y = X[:m/2+1] + np.r_[0,X[m/2+1:],0]*1j



![png](/img/ds/seaborn/output_13_1.png)


### Adding a Legend


```python
g = sns.FacetGrid(titanic, col="Survived", row="Pclass", hue="Sex")
g.map(sns.kdeplot, "Age", shade=True).add_legend()
sns.despine(left=True, bottom = True)
plt.show()

```

    E:\Anaconda3\lib\site-packages\statsmodels\nonparametric\kdetools.py:20: VisibleDeprecationWarning: using a non-integer number instead of an integer will result in an error in the future
      y = X[:m/2+1] + np.r_[0,X[m/2+1:],0]*1j



![png](/img/ds/seaborn/output_15_1.png)


http://seaborn.pydata.org/generated/seaborn.FacetGrid.html#seaborn.FacetGrid


```python

```
