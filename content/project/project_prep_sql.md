+++
# Date this page was created.
date = "2017-04-27"

# Project title.
title = "Preparing the data to use it in a mySQL database."

# Project summary to display on homepage.
summary = "In this project we are going to preapare and serve the data into a mySQL database."

# Optional image to display on homepage (relative to `static/img/headers` folder).
image_preview = "/python-mysql.png"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["datascience"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "headers/python-mysql.png"
caption = "Making them work together."

+++



# Preparing Data to use it in a mySQL database

#### In this project we are going to preapare and serve the data into a mySQL database.


```python
import pandas as pd

df = pd.read_csv("academy_awards.csv", encoding="ISO-8859-1")
df
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
      <th>Year</th>
      <th>Category</th>
      <th>Nominee</th>
      <th>Additional Info</th>
      <th>Won?</th>
      <th>Unnamed: 5</th>
      <th>Unnamed: 6</th>
      <th>Unnamed: 7</th>
      <th>Unnamed: 8</th>
      <th>Unnamed: 9</th>
      <th>Unnamed: 10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010 (83rd)</td>
      <td>Actor -- Leading Role</td>
      <td>Javier Bardem</td>
      <td>Biutiful {'Uxbal'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010 (83rd)</td>
      <td>Actor -- Leading Role</td>
      <td>Jeff Bridges</td>
      <td>True Grit {'Rooster Cogburn'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010 (83rd)</td>
      <td>Actor -- Leading Role</td>
      <td>Jesse Eisenberg</td>
      <td>The Social Network {'Mark Zuckerberg'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010 (83rd)</td>
      <td>Actor -- Leading Role</td>
      <td>Colin Firth</td>
      <td>The King's Speech {'King George VI'}</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010 (83rd)</td>
      <td>Actor -- Leading Role</td>
      <td>James Franco</td>
      <td>127 Hours {'Aron Ralston'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2010 (83rd)</td>
      <td>Actor -- Supporting Role</td>
      <td>Christian Bale</td>
      <td>The Fighter {'Dicky Eklund'}</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2010 (83rd)</td>
      <td>Actor -- Supporting Role</td>
      <td>John Hawkes</td>
      <td>Winter's Bone {'Teardrop'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2010 (83rd)</td>
      <td>Actor -- Supporting Role</td>
      <td>Jeremy Renner</td>
      <td>The Town {'James Coughlin'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2010 (83rd)</td>
      <td>Actor -- Supporting Role</td>
      <td>Mark Ruffalo</td>
      <td>The Kids Are All Right {'Paul'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2010 (83rd)</td>
      <td>Actor -- Supporting Role</td>
      <td>Geoffrey Rush</td>
      <td>The King's Speech {'Lionel Logue'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2010 (83rd)</td>
      <td>Actress -- Leading Role</td>
      <td>Annette Bening</td>
      <td>The Kids Are All Right {'Nic'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2010 (83rd)</td>
      <td>Actress -- Leading Role</td>
      <td>Nicole Kidman</td>
      <td>Rabbit Hole {'Becca'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2010 (83rd)</td>
      <td>Actress -- Leading Role</td>
      <td>Jennifer Lawrence</td>
      <td>Winter's Bone {'Ree'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2010 (83rd)</td>
      <td>Actress -- Leading Role</td>
      <td>Natalie Portman</td>
      <td>Black Swan {'Nina Sayers/The Swan Queen'}</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2010 (83rd)</td>
      <td>Actress -- Leading Role</td>
      <td>Michelle Williams</td>
      <td>Blue Valentine {'Cindy'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2010 (83rd)</td>
      <td>Actress -- Supporting Role</td>
      <td>Amy Adams</td>
      <td>The Fighter {'Charlene Fleming'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2010 (83rd)</td>
      <td>Actress -- Supporting Role</td>
      <td>Helena Bonham Carter</td>
      <td>The King's Speech {'Queen Elizabeth'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2010 (83rd)</td>
      <td>Actress -- Supporting Role</td>
      <td>Melissa Leo</td>
      <td>The Fighter {'Alice Ward'}</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2010 (83rd)</td>
      <td>Actress -- Supporting Role</td>
      <td>Hailee Steinfeld</td>
      <td>True Grit {'Mattie Ross'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2010 (83rd)</td>
      <td>Actress -- Supporting Role</td>
      <td>Jacki Weaver</td>
      <td>Animal Kingdom {'Janine 'Smurf' Cody'}</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2010 (83rd)</td>
      <td>Animated Feature Film</td>
      <td>How to Train Your Dragon</td>
      <td>Chris Sanders and Dean DeBlois</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2010 (83rd)</td>
      <td>Animated Feature Film</td>
      <td>The Illusionist</td>
      <td>Sylvain Chomet</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2010 (83rd)</td>
      <td>Animated Feature Film</td>
      <td>Toy Story 3</td>
      <td>Lee Unkrich</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2010 (83rd)</td>
      <td>Art Direction</td>
      <td>Alice in Wonderland</td>
      <td>Production Design: Robert Stromberg; Set Decor...</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2010 (83rd)</td>
      <td>Art Direction</td>
      <td>Harry Potter and the Deathly Hallows Part 1</td>
      <td>Production Design: Stuart Craig; Set Decoratio...</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2010 (83rd)</td>
      <td>Art Direction</td>
      <td>Inception</td>
      <td>Production Design: Guy Hendrix Dyas; Set Decor...</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2010 (83rd)</td>
      <td>Art Direction</td>
      <td>The King's Speech</td>
      <td>Production Design: Eve Stewart; Set Decoration...</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2010 (83rd)</td>
      <td>Art Direction</td>
      <td>True Grit</td>
      <td>Production Design: Jess Gonchor; Set Decoratio...</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2010 (83rd)</td>
      <td>Cinematography</td>
      <td>Black Swan</td>
      <td>Matthew Libatique</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2010 (83rd)</td>
      <td>Cinematography</td>
      <td>Inception</td>
      <td>Wally Pfister</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>10107</th>
      <td>1927/28 (1st)</td>
      <td>Art Direction</td>
      <td>Harry Oliver</td>
      <td>7th Heaven</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10108</th>
      <td>1927/28 (1st)</td>
      <td>Cinematography</td>
      <td>George Barnes</td>
      <td>The Devil Dancer; The Magic Flame; and Sadie T...</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10109</th>
      <td>1927/28 (1st)</td>
      <td>Cinematography</td>
      <td>Charles Rosher</td>
      <td>Sunrise</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10110</th>
      <td>1927/28 (1st)</td>
      <td>Cinematography</td>
      <td>Karl Struss</td>
      <td>Sunrise</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10111</th>
      <td>1927/28 (1st)</td>
      <td>Directing</td>
      <td>Lewis Milestone</td>
      <td>Two Arabian Knights</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10112</th>
      <td>1927/28 (1st)</td>
      <td>Directing</td>
      <td>Ted Wilde</td>
      <td>Speedy</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10113</th>
      <td>1927/28 (1st)</td>
      <td>Directing</td>
      <td>Frank Borzage</td>
      <td>7th Heaven</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10114</th>
      <td>1927/28 (1st)</td>
      <td>Directing</td>
      <td>Herbert Brenon</td>
      <td>Sorrell and Son</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10115</th>
      <td>1927/28 (1st)</td>
      <td>Directing</td>
      <td>King Vidor</td>
      <td>The Crowd</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10116</th>
      <td>1927/28 (1st)</td>
      <td>Directing</td>
      <td>To Charles Chaplin, for acting, writing, direc...</td>
      <td>NaN</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10117</th>
      <td>1927/28 (1st)</td>
      <td>Best Picture</td>
      <td>The Caddo Company</td>
      <td>The Racket</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10118</th>
      <td>1927/28 (1st)</td>
      <td>Best Picture</td>
      <td>Fox</td>
      <td>7th Heaven</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10119</th>
      <td>1927/28 (1st)</td>
      <td>Best Picture</td>
      <td>Paramount Famous Lasky</td>
      <td>Wings</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10120</th>
      <td>1927/28 (1st)</td>
      <td>Writing</td>
      <td>Alfred Cohn</td>
      <td>The Jazz Singer</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10121</th>
      <td>1927/28 (1st)</td>
      <td>Writing</td>
      <td>Anthony Coldeway</td>
      <td>Glorious Betsy</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10122</th>
      <td>1927/28 (1st)</td>
      <td>Writing</td>
      <td>Benjamin Glazer</td>
      <td>7th Heaven</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10123</th>
      <td>1927/28 (1st)</td>
      <td>Writing</td>
      <td>Lajos Biro</td>
      <td>The Last Command</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10124</th>
      <td>1927/28 (1st)</td>
      <td>Writing</td>
      <td>Ben Hecht</td>
      <td>Underworld</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10125</th>
      <td>1927/28 (1st)</td>
      <td>Writing</td>
      <td>Gerald Duffy</td>
      <td>The Private Life of Helen of Troy</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10126</th>
      <td>1927/28 (1st)</td>
      <td>Writing</td>
      <td>Joseph Farnham[NOTE: This award was not associ...</td>
      <td>NaN</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10127</th>
      <td>1927/28 (1st)</td>
      <td>Writing</td>
      <td>George Marion, Jr.[NOTE: This nomination was n...</td>
      <td>NaN</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10128</th>
      <td>1927/28 (1st)</td>
      <td>Writing</td>
      <td>To Charles Chaplin, for acting, writing, direc...</td>
      <td>NaN</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10129</th>
      <td>1927/28 (1st)</td>
      <td>Honorary Award</td>
      <td>To Warner Bros., for producing The Jazz Singer...</td>
      <td>NaN</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10130</th>
      <td>1927/28 (1st)</td>
      <td>Honorary Award</td>
      <td>To Charles Chaplin, for acting, writing, direc...</td>
      <td>NaN</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10131</th>
      <td>1927/28 (1st)</td>
      <td>Engineering Effects (archaic category)</td>
      <td>Ralph Hammeras [NOTE: This nomination was not ...</td>
      <td>NaN</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10132</th>
      <td>1927/28 (1st)</td>
      <td>Engineering Effects (archaic category)</td>
      <td>Roy Pomeroy</td>
      <td>Wings</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10133</th>
      <td>1927/28 (1st)</td>
      <td>Engineering Effects (archaic category)</td>
      <td>Nugent Slaughter [NOTE: Though no specific tit...</td>
      <td>NaN</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10134</th>
      <td>1927/28 (1st)</td>
      <td>Unique and Artistic Picture (archaic category)</td>
      <td>Fox</td>
      <td>Sunrise</td>
      <td>YES</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10135</th>
      <td>1927/28 (1st)</td>
      <td>Unique and Artistic Picture (archaic category)</td>
      <td>Metro-Goldwyn-Mayer</td>
      <td>The Crowd</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10136</th>
      <td>1927/28 (1st)</td>
      <td>Unique and Artistic Picture (archaic category)</td>
      <td>Paramount Famous Lasky</td>
      <td>Chang</td>
      <td>NO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>10137 rows × 11 columns</p>
</div>




```python
df.ix[5].value_counts()
```

    C:\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: DeprecationWarning:
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing

    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#deprecate_ix
      """Entry point for launching an IPython kernel.





    Christian Bale                  1
    YES                             1
    Actor -- Supporting Role        1
    The Fighter {'Dicky Eklund'}    1
    2010 (83rd)                     1
    Name: 5, dtype: int64



# Filtering The Data


```python
df['Year'] = df['Year'].str[0:4]
df['Year'] = df['Year'].astype('int64')

later_than_2000 = df[df['Year'] > 2000]
award_categories = ['Actor -- Leading Role', 'Actor -- Supporting Role', 'Actress -- Leading Role', 'Actress -- Supporting Role']

nominations = later_than_2000[later_than_2000["Category"].isin(award_categories)]

print(nominations.head())
```

       Year               Category          Nominee  \
    0  2010  Actor -- Leading Role    Javier Bardem   
    1  2010  Actor -- Leading Role     Jeff Bridges   
    2  2010  Actor -- Leading Role  Jesse Eisenberg   
    3  2010  Actor -- Leading Role      Colin Firth   
    4  2010  Actor -- Leading Role     James Franco   

                              Additional Info Won? Unnamed: 5 Unnamed: 6  \
    0                      Biutiful {'Uxbal'}   NO        NaN        NaN   
    1           True Grit {'Rooster Cogburn'}   NO        NaN        NaN   
    2  The Social Network {'Mark Zuckerberg'}   NO        NaN        NaN   
    3    The King's Speech {'King George VI'}  YES        NaN        NaN   
    4              127 Hours {'Aron Ralston'}   NO        NaN        NaN   

      Unnamed: 7 Unnamed: 8 Unnamed: 9 Unnamed: 10  
    0        NaN        NaN        NaN         NaN  
    1        NaN        NaN        NaN         NaN  
    2        NaN        NaN        NaN         NaN  
    3        NaN        NaN        NaN         NaN  
    4        NaN        NaN        NaN         NaN  


# Cleaning Up The Won? And Unnamed Columns


```python
pd.options.mode.chained_assignment = None # default='warn'
replace_dict = {'NO': 0, 'YES': 1}
nominations['Won?'] = nominations['Won?'].map(replace_dict)
nominations['Won'] = nominations['Won?']
drop_cols = ['Won?', 'Unnamed: 5', 'Unnamed: 6', 'Unnamed: 7', 'Unnamed: 8', 'Unnamed: 9', 'Unnamed: 10']

final_nominations = nominations.drop(drop_cols, axis=1)
final_nominations.head()
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
      <th>Year</th>
      <th>Category</th>
      <th>Nominee</th>
      <th>Additional Info</th>
      <th>Won</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>Actor -- Leading Role</td>
      <td>Javier Bardem</td>
      <td>Biutiful {'Uxbal'}</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010</td>
      <td>Actor -- Leading Role</td>
      <td>Jeff Bridges</td>
      <td>True Grit {'Rooster Cogburn'}</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010</td>
      <td>Actor -- Leading Role</td>
      <td>Jesse Eisenberg</td>
      <td>The Social Network {'Mark Zuckerberg'}</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010</td>
      <td>Actor -- Leading Role</td>
      <td>Colin Firth</td>
      <td>The King's Speech {'King George VI'}</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010</td>
      <td>Actor -- Leading Role</td>
      <td>James Franco</td>
      <td>127 Hours {'Aron Ralston'}</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



# Cleaning Up The Additional Info Column

- The values in this column contain the movie name and the character the nominee played. Instead of keeping these values in 1 column, split them up into 2 different columns for easier querying.


```python
additional_info_one = final_nominations['Additional Info'].str.rstrip("'}")
additional_info_two = additional_info_one.str.split(" {'")
movie_names = additional_info_two.str[0]
characters = additional_info_two.str[1]

final_nominations['Movie'] = movie_names
final_nominations['Character'] = characters

final_nominations = final_nominations.drop("Additional Info", axis=1)
final_nominations.head()

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
      <th>Year</th>
      <th>Category</th>
      <th>Nominee</th>
      <th>Won</th>
      <th>Movie</th>
      <th>Character</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>Actor -- Leading Role</td>
      <td>Javier Bardem</td>
      <td>0</td>
      <td>Biutiful</td>
      <td>Uxbal</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010</td>
      <td>Actor -- Leading Role</td>
      <td>Jeff Bridges</td>
      <td>0</td>
      <td>True Grit</td>
      <td>Rooster Cogburn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010</td>
      <td>Actor -- Leading Role</td>
      <td>Jesse Eisenberg</td>
      <td>0</td>
      <td>The Social Network</td>
      <td>Mark Zuckerberg</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010</td>
      <td>Actor -- Leading Role</td>
      <td>Colin Firth</td>
      <td>1</td>
      <td>The King's Speech</td>
      <td>King George VI</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010</td>
      <td>Actor -- Leading Role</td>
      <td>James Franco</td>
      <td>0</td>
      <td>127 Hours</td>
      <td>Aron Ralston</td>
    </tr>
  </tbody>
</table>
</div>



# Exporting To SQLite


```python
import sqlite3

conn = sqlite3.connect("nominations.db")
final_nominations.to_sql("nominations", conn, index=False)

```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-8-102f757f32a4> in <module>()
          2
          3 conn = sqlite3.connect("nominations.db")
    ----> 4 final_nominations.to_sql("nominations", conn, index=False)


    C:\Anaconda3\lib\site-packages\pandas\core\generic.py in to_sql(self, name, con, flavor, schema, if_exists, index, index_label, chunksize, dtype)
       1343         sql.to_sql(self, name, con, flavor=flavor, schema=schema,
       1344                    if_exists=if_exists, index=index, index_label=index_label,
    -> 1345                    chunksize=chunksize, dtype=dtype)
       1346
       1347     def to_pickle(self, path, compression='infer'):


    C:\Anaconda3\lib\site-packages\pandas\io\sql.py in to_sql(frame, name, con, flavor, schema, if_exists, index, index_label, chunksize, dtype)
        469     pandas_sql.to_sql(frame, name, if_exists=if_exists, index=index,
        470                       index_label=index_label, schema=schema,
    --> 471                       chunksize=chunksize, dtype=dtype)
        472
        473


    C:\Anaconda3\lib\site-packages\pandas\io\sql.py in to_sql(self, frame, name, if_exists, index, index_label, schema, chunksize, dtype)
       1503                             if_exists=if_exists, index_label=index_label,
       1504                             dtype=dtype)
    -> 1505         table.create()
       1506         table.insert(chunksize)
       1507


    C:\Anaconda3\lib\site-packages\pandas\io\sql.py in create(self)
        586         if self.exists():
        587             if self.if_exists == 'fail':
    --> 588                 raise ValueError("Table '%s' already exists." % self.name)
        589             elif self.if_exists == 'replace':
        590                 self.pd_sql.drop_table(self.name, self.schema)


    ValueError: Table 'nominations' already exists.


# Verifying In SQL


```python
query_one = "PRAGMA table_info(nominations)"
query_two = "select * from nominations limit 10"
print(conn.execute(query_one).fetchall())
print(conn.execute(query_two).fetchall())
conn.close()
```
