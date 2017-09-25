+++
# Date this page was created.
date = "2017-04-27"

# Project title.
title = "Visualizing the gender gap in Major College Degrees"

# Project summary to display on homepage.
summary = "In this project we are going check which gender predominates in every major degree and also, we are going to see the tendency that it folows."

# Optional image to display on homepage (relative to `static/img/headers` folder).
image_preview = "gendergap.png"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["datascience"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "ds/gendergap/output_1_0.png"
caption = "Gender gap tendency, looking at how it is changing."

+++


# Visualizing the gender Gap in College



```python
%matplotlib inline
import pandas as pd
import matplotlib.pyplot as plt

women_degrees = pd.read_csv('percent-bachelors-degrees-women-usa.csv')
cb_dark_blue = (0/255,107/255,164/255)
cb_orange = (255/255, 128/255, 14/255)
stem_cats = ['Engineering', 'Computer Science', 'Psychology', 'Biology', 'Physical Sciences', 'Math and Statistics']

fig = plt.figure(figsize=(18, 3))

for sp in range(0,6):
    ax = fig.add_subplot(1,6,sp+1)
    ax.plot(women_degrees['Year'], women_degrees[stem_cats[sp]], c=cb_dark_blue, label='Women', linewidth=3)
    ax.plot(women_degrees['Year'], 100-women_degrees[stem_cats[sp]], c=cb_orange, label='Men', linewidth=3)
    ax.spines["right"].set_visible(False)    
    ax.spines["left"].set_visible(False)
    ax.spines["top"].set_visible(False)    
    ax.spines["bottom"].set_visible(False)
    ax.set_xlim(1968, 2011)
    ax.set_ylim(0,100)
    ax.set_title(stem_cats[sp])
    ax.tick_params(bottom="off", top="off", left="off", right="off")

    if sp == 0:
        ax.text(2005, 87, 'Men')
        ax.text(2002, 8, 'Women')
    elif sp == 5:
        ax.text(2005, 62, 'Men')
        ax.text(2001, 35, 'Women')
plt.show()
```


![png](/img/ds/gendergap/output_1_0.png)



```python
#Data for this plots
stem_cats = ['Psychology', 'Biology', 'Math and Statistics', 'Physical Sciences', 'Computer Science', 'Engineering', 'Computer Science']
lib_arts_cats = ['Foreign Languages', 'English', 'Communications and Journalism', 'Art and Performance', 'Social Sciences and History']
other_cats = ['Health Professions', 'Public Administration', 'Education', 'Agriculture','Business', 'Architecture']


fig = plt.figure(figsize=(16, 16))
count_stem = 0
count_lib_arts = 0
count_other = 0

#First column, STEM degrees
for sp in range(0, 18, 3):
    ax = fig.add_subplot(6, 3, sp+1)
    ax.plot(women_degrees['Year'], women_degrees[stem_cats[count_stem]], c=cb_dark_blue, label="Women", linewidth=3)
    ax.plot(women_degrees['Year'], 100-women_degrees[stem_cats[count_stem]], c= cb_orange, label="Men", linewidth=3)
    ax.set_xlim(1970, 2010)
    ax.set_ylim(0, 100)
    ax.set_title(stem_cats[count_stem])
    ax.tick_params(bottom = "off", left = "off", top = "off", right = "off")
    ax.spines["right"].set_visible(False)    
    ax.spines["left"].set_visible(False)
    ax.spines["top"].set_visible(False)    
    ax.spines["bottom"].set_visible(False)
    ax.tick_params(labelbottom='off')
    ax.set_yticks([0, 100])
    ax.axhline(50, c=(171/255, 171/255, 171/255), alpha = 0.3)
    if count_stem == 0:
        ax.text(2006, 80, "Women")
        ax.text(2006, 10, "Men")
    if count_stem == 5:
        ax.text(2006, 90, "Women")
        ax.text(2006, 25, "Men")
        ax.tick_params(labelbottom='on')
    count_stem += 1


#Second Column. Liberal Arts.
for sp in range(1, 16, 3):
    ax = fig.add_subplot(6, 3, sp+1)
    ax.plot(women_degrees['Year'], women_degrees[lib_arts_cats[count_lib_arts]], c=cb_dark_blue, label="Women", linewidth=3)
    ax.plot(women_degrees['Year'], 100-women_degrees[lib_arts_cats[count_lib_arts]], c=cb_orange, label="Men", linewidth=3)
    ax.set_xlim(1970, 2010)
    ax.set_ylim(0, 100)
    ax.set_title(lib_arts_cats[count_lib_arts])
    ax.tick_params(bottom = "off", left = "off", top = "off", right = "off")
    ax.spines["right"].set_visible(False)    
    ax.spines["left"].set_visible(False)
    ax.spines["top"].set_visible(False)    
    ax.spines["bottom"].set_visible(False)
    ax.tick_params(labelbottom='off')
    ax.set_yticks([0, 100])
    ax.axhline(50, c=(171/255, 171/255, 171/255), alpha = 0.3)
    if count_lib_arts == 0:
        ax.text(2006, 80, "Women")
        ax.text(2006, 10, "Men")
    if count_lib_arts == 4:
        ax.text(2006, 90, "Women")
        ax.text(2006, 25, "Men")
        ax.tick_params(labelbottom='on')

    count_lib_arts += 1

#Third Column. Other cats.
for sp in range(2, 20, 3):
    ax = fig.add_subplot(6, 3, sp+1)
    ax.plot(women_degrees['Year'], women_degrees[other_cats[count_other]], c=cb_dark_blue, label = "Women", linewidth = 3)
    ax.plot(women_degrees['Year'], 100-women_degrees[other_cats[count_other]], c=cb_orange, label = "Men", linewidth = 3)    
    ax.set_xlim(1970, 2010)
    ax.set_ylim(0, 100)
    ax.set_title(other_cats[count_other])
    ax.tick_params(bottom = "off", left = "off", top = "off", right = "off")
    ax.spines["right"].set_visible(False)    
    ax.spines["left"].set_visible(False)
    ax.spines["top"].set_visible(False)    
    ax.spines["bottom"].set_visible(False)
    ax.tick_params(labelbottom='off')
    ax.set_yticks([0, 100])
    ax.axhline(50, c=(171/255, 171/255, 171/255), alpha = 0.3)
    if count_other == 0:
        ax.text(2006, 90, "Women")
        ax.text(2006, 4, "Men")
    if count_other == 5:
        ax.text(2006, 80, "Women")
        ax.text(2006, 25, "Men")
        ax.tick_params(labelbottom='on')


    count_other += 1

plt.savefig("gender_degrees.png")
plt.show()
```


![png](/img/ds/gendergap/output_2_0.png)


# Conclusions:

- We can certainly apreciate that while still some majors predominated by one of the genders, the tendency is to equally be studied by both as we can see with the progression os certain subjects like social sciences, business, and we can predict that in future the difference encountered in engineering will be less notable.


```python

```
