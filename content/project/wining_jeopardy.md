+++
# Date this page was created.
date = "2017-04-27"

# Project title.
title = "Winning at Jeopardy Game (part 1/2) "

# Project summary to display on homepage.
summary = "- In this project we are going to first:- Normalize the text.- Look for the answers in questions.- Look for question that are repeated from time to time. (Trying to win easy :)- Low Value & high Value Question. How to get more points.- Applying the Chi-Squared Test. "

# Optional image to display on homepage (relative to `static/img/headers` folder).
image_preview = "jeopardy.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["datascience"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "headers/jeopardy.jpg"
caption = ""

+++



# Winning at Jeopardy Game (part 1/2)

#### Jeopardy! es un concurso de televisión estadounidense creado por Merv Griffin. Es un concurso de conocimientos con preguntas sobre numerosos temas como historia, idiomas, literatura, cultura popular, bellas artes, ciencia, geografía, y deportes. Consiste en que uno de los tres concursantes elige uno de los paneles del tablero de juego, el cual, al ser descubierto, revela una pista en forma de respuesta; los concursantes entonces tienen que dar sus respuestas en forma de una pregunta.

- In this project we are going to first:
    - Normalize the text.
    - Look for the answers in questions.
    - Look for question that are repeated from time to time. (Trying to win easy :)
    - Low Value & high Value Question. How to get more points.
    - Applying the Chi-Squared Test.


```python
import pandas as pd
import csv

jeopardy = pd.read_csv("jeopardy.csv")

print(jeopardy.head())
```

       Show Number    Air Date      Round                         Category  Value  \
    0         4680  2004-12-31  Jeopardy!                          HISTORY   $200   
    1         4680  2004-12-31  Jeopardy!  ESPN's TOP 10 ALL-TIME ATHLETES   $200   
    2         4680  2004-12-31  Jeopardy!      EVERYBODY TALKS ABOUT IT...   $200   
    3         4680  2004-12-31  Jeopardy!                 THE COMPANY LINE   $200   
    4         4680  2004-12-31  Jeopardy!              EPITAPHS & TRIBUTES   $200   

                                                Question      Answer  
    0  For the last 8 years of his life, Galileo was ...  Copernicus  
    1  No. 2: 1912 Olympian; football star at Carlisl...  Jim Thorpe  
    2  The city of Yuma in this state has a record av...     Arizona  
    3  In 1963, live on "The Art Linkletter Show", th...  McDonald's  
    4  Signer of the Dec. of Indep., framer of the Co...  John Adams  



```python
jeopardy.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Show Number</th>
      <th>Air Date</th>
      <th>Round</th>
      <th>Category</th>
      <th>Value</th>
      <th>Question</th>
      <th>Answer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4680</td>
      <td>2004-12-31</td>
      <td>Jeopardy!</td>
      <td>HISTORY</td>
      <td>$200</td>
      <td>For the last 8 years of his life, Galileo was ...</td>
      <td>Copernicus</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4680</td>
      <td>2004-12-31</td>
      <td>Jeopardy!</td>
      <td>ESPN's TOP 10 ALL-TIME ATHLETES</td>
      <td>$200</td>
      <td>No. 2: 1912 Olympian; football star at Carlisl...</td>
      <td>Jim Thorpe</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4680</td>
      <td>2004-12-31</td>
      <td>Jeopardy!</td>
      <td>EVERYBODY TALKS ABOUT IT...</td>
      <td>$200</td>
      <td>The city of Yuma in this state has a record av...</td>
      <td>Arizona</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4680</td>
      <td>2004-12-31</td>
      <td>Jeopardy!</td>
      <td>THE COMPANY LINE</td>
      <td>$200</td>
      <td>In 1963, live on "The Art Linkletter Show", th...</td>
      <td>McDonald's</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4680</td>
      <td>2004-12-31</td>
      <td>Jeopardy!</td>
      <td>EPITAPHS &amp; TRIBUTES</td>
      <td>$200</td>
      <td>Signer of the Dec. of Indep., framer of the Co...</td>
      <td>John Adams</td>
    </tr>
  </tbody>
</table>
</div>




```python
jeopardy.columns
```




    Index(['Show Number', ' Air Date', ' Round', ' Category', ' Value',
           ' Question', ' Answer'],
          dtype='object')




```python
jeopardy.columns = ['Show Number', 'Air Date', 'Round', 'Category', 'Value', 'Question', 'Answer']
jeopardy.columns
```




    Index(['Show Number', 'Air Date', 'Round', 'Category', 'Value', 'Question',
           'Answer'],
          dtype='object')



# Normalizing Text


```python
import re

def normalize_text(text):
    text = text.lower()
    text = re.sub("[^A-Za-z0-9\s]", "", text)
    return text

def normalize_values(text):
    text = re.sub("[^A-Za-z0-9\s]", "", text)

    try:
        text = int(text)
    except Exception:
        text = 0
    return text

```


```python
jeopardy["clean_question"] = jeopardy["Question"].apply(normalize_text)
jeopardy["clean_answer"] = jeopardy["Answer"].apply(normalize_text)
jeopardy["clean_value"] = jeopardy["Value"].apply(normalize_values)
```


```python
jeopardy.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Show Number</th>
      <th>Air Date</th>
      <th>Round</th>
      <th>Category</th>
      <th>Value</th>
      <th>Question</th>
      <th>Answer</th>
      <th>clean_question</th>
      <th>clean_answer</th>
      <th>clean_value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4680</td>
      <td>2004-12-31</td>
      <td>Jeopardy!</td>
      <td>HISTORY</td>
      <td>$200</td>
      <td>For the last 8 years of his life, Galileo was ...</td>
      <td>Copernicus</td>
      <td>for the last 8 years of his life galileo was u...</td>
      <td>copernicus</td>
      <td>200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4680</td>
      <td>2004-12-31</td>
      <td>Jeopardy!</td>
      <td>ESPN's TOP 10 ALL-TIME ATHLETES</td>
      <td>$200</td>
      <td>No. 2: 1912 Olympian; football star at Carlisl...</td>
      <td>Jim Thorpe</td>
      <td>no 2 1912 olympian football star at carlisle i...</td>
      <td>jim thorpe</td>
      <td>200</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4680</td>
      <td>2004-12-31</td>
      <td>Jeopardy!</td>
      <td>EVERYBODY TALKS ABOUT IT...</td>
      <td>$200</td>
      <td>The city of Yuma in this state has a record av...</td>
      <td>Arizona</td>
      <td>the city of yuma in this state has a record av...</td>
      <td>arizona</td>
      <td>200</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4680</td>
      <td>2004-12-31</td>
      <td>Jeopardy!</td>
      <td>THE COMPANY LINE</td>
      <td>$200</td>
      <td>In 1963, live on "The Art Linkletter Show", th...</td>
      <td>McDonald's</td>
      <td>in 1963 live on the art linkletter show this c...</td>
      <td>mcdonalds</td>
      <td>200</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4680</td>
      <td>2004-12-31</td>
      <td>Jeopardy!</td>
      <td>EPITAPHS &amp; TRIBUTES</td>
      <td>$200</td>
      <td>Signer of the Dec. of Indep., framer of the Co...</td>
      <td>John Adams</td>
      <td>signer of the dec of indep framer of the const...</td>
      <td>john adams</td>
      <td>200</td>
    </tr>
  </tbody>
</table>
</div>




```python
jeopardy["Air Date"] = pd.to_datetime(jeopardy["Air Date"])
```


```python
jeopardy.dtypes
```




    Show Number                int64
    Air Date          datetime64[ns]
    Round                     object
    Category                  object
    Value                     object
    Question                  object
    Answer                    object
    clean_question            object
    clean_answer              object
    clean_value                int64
    dtype: object



# Looking for Answers in Questions


```python
def answ_in_quest(row):
    split_answer = row["clean_answer"].split(" ")
    split_question = row["clean_question"].split(" ")

    match_count = 0

    if "the" in split_answer:
        split_answer.remove('the')
    if len(split_answer) == 0:
        return 0

    for item in split_answer:
        if item in split_question:
            match_count += 1

    return match_count / len(split_answer)

jeopardy['answer_in_question'] = jeopardy.apply(answ_in_quest, axis=1)

```


```python
jeopardy["answer_in_question"].mean()
```




    0.060493257069335872



### The percentage of finding the answer in the question is around 6%, as it is a small quantity in order to win at this game we cannot expect to get a los of answers just looking at the question.

# Looking for Questions that are repeated from time to time


```python
question_overlap = []
terms_used = set()

for i, row in jeopardy.iterrows():
    split_question = row["clean_question"].split(" ")

    split_question = [q for q in split_question if len(q) > 5]
    match_count = 0

    for word in split_question:
        if word in terms_used:
            match_count += 1
        terms_used.add(word)

    if len(split_question) > 0:
        match_count = match_count/len(split_question)

    question_overlap.append(match_count)

jeopardy["question_overlap"] = question_overlap

jeopardy["question_overlap"].mean()
```




    0.69259600573386471



#### Here we have a mean of 70% which means that it can be relevant to look at past question because is probably that it would be repeated in other games, but here we hav to be careful because we look at it by word per word which cna be tricky, but definetly, the 70% is significant and we should keep working in this part of the game.

# Low Value Vs High Value Questions


```python
def assign_values(row):
    if row['clean_value'] > 800:
        value = 1
    else:
        value = 0
    return value
jeopardy['high_value'] = jeopardy.apply(assign_values, axis = 1)
```


```python
def takes_a_word(word):
    low_count = 0
    high_count = 0

    for i, row in jeopardy.iterrows():
        split_question = row["clean_question"].split(" ")

        if word in split_question:
            if row['high_value'] == 1:
                high_count += 1
            else:
                low_count += 1
    return high_count, low_count

```


```python
observed_expected = []

comparison_terms = list(terms_used)[:5]
```


```python
print(comparison_terms)
```

    ['glamourous', 'handsomest', 'sutherland', 'laptopa', 'absorbed']



```python
for term in comparison_terms:
    observed_expected.append(takes_a_word(term))
```


```python
observed_expected
```




    [(1, 0), (1, 1), (0, 1), (0, 1), (2, 0)]



# Applying The Chi-Squared Test


```python
high_value_count = jeopardy[jeopardy["high_value"] == 1].shape[0]
print(high_value_count)
```

    5734



```python
low_value_count = jeopardy[jeopardy["high_value"] == 0].shape[0]
```


```python
chi_squared = []

from scipy.stats import chisquare
import numpy as np
```


```python
for obs in observed_expected:
    total = sum(obs)
    total_prop = total / len(jeopardy)
    exp_high_value = total_prop * high_value_count
    exp_low_value = total_prop * low_value_count

    chi_squared.append(chisquare(np.array([obs[0], obs[1]]), np.array([exp_high_value, exp_low_value])))
```


```python
chi_squared
```




    [Power_divergenceResult(statistic=2.4877921171956752, pvalue=0.11473257634454047),
     Power_divergenceResult(statistic=0.44487748166127949, pvalue=0.50477764875459963),
     Power_divergenceResult(statistic=0.40196284612688399, pvalue=0.52607729857054686),
     Power_divergenceResult(statistic=0.40196284612688399, pvalue=0.52607729857054686),
     Power_divergenceResult(statistic=4.9755842343913503, pvalue=0.025707519787911092),
     Power_divergenceResult(statistic=2.4877921171956752, pvalue=0.11473257634454047),
     Power_divergenceResult(statistic=0.44487748166127949, pvalue=0.50477764875459963),
     Power_divergenceResult(statistic=0.40196284612688399, pvalue=0.52607729857054686),
     Power_divergenceResult(statistic=0.40196284612688399, pvalue=0.52607729857054686),
     Power_divergenceResult(statistic=4.9755842343913503, pvalue=0.025707519787911092)]



#### We will continue in part 2 trying different model to get some more insights and se if they can work better than chi-Squared.


```python

```
