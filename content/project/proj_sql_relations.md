+++
# Date this page was created.
date = "2017-04-27"

# Project title.
title = "Creating Relations in SQL database and Python."

# Project summary to display on homepage.
summary = "In this project we are going to work with SQL and Python, creating tables, foreign keys, setting up relations, one to many, many to many and deleting and joining tables wwith Join"

# Optional image to display on homepage (relative to `static/img/headers` folder).
image_preview = "/sqlite3_relations.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["datascience"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = ""
caption = ""

+++



# Creating Relations in SQL and Python

### In this project we are going to create relations using Sqlite3 and python, we are going to:

[TOC]

#### Creating The Ceremonies Table
#### Foreign Key Constraints
#### Setting Up One-To-Many
#### Deleting And Renaming Tables
#### Creating A Join Table



```python
import sqlite3

conn = sqlite3.connect("nominations.db")
```


```python
schema = conn.execute("PRAGMA table_info(nominations);").fetchall()
```


```python
first_ten = conn.execute("SELECT * FROM nominations LIMIT 10;").fetchall()
for s in schema:
    print(s)

for row in first_ten:
    print(row)
```

    (0, 'Year', 'INTEGER', 0, None, 0)
    (1, 'Category', 'TEXT', 0, None, 0)
    (2, 'Nominee', 'TEXT', 0, None, 0)
    (3, 'Won', 'INTEGER', 0, None, 0)
    (4, 'Movie', 'TEXT', 0, None, 0)
    (5, 'Character', 'TEXT', 0, None, 0)
    (2010, 'Actor -- Leading Role', 'Javier Bardem', 0, 'Biutiful', 'Uxbal')
    (2010, 'Actor -- Leading Role', 'Jeff Bridges', 0, 'True Grit', 'Rooster Cogburn')
    (2010, 'Actor -- Leading Role', 'Jesse Eisenberg', 0, 'The Social Network', 'Mark Zuckerberg')
    (2010, 'Actor -- Leading Role', 'Colin Firth', 1, "The King's Speech", 'King George VI')
    (2010, 'Actor -- Leading Role', 'James Franco', 0, '127 Hours', 'Aron Ralston')
    (2010, 'Actor -- Supporting Role', 'Christian Bale', 1, 'The Fighter', 'Dicky Eklund')
    (2010, 'Actor -- Supporting Role', 'John Hawkes', 0, "Winter's Bone", 'Teardrop')
    (2010, 'Actor -- Supporting Role', 'Jeremy Renner', 0, 'The Town', 'James Coughlin')
    (2010, 'Actor -- Supporting Role', 'Mark Ruffalo', 0, 'The Kids Are All Right', 'Paul')
    (2010, 'Actor -- Supporting Role', 'Geoffrey Rush', 0, "The King's Speech", 'Lionel Logue')


# Creating The Ceremonies Table


```python
years_hosts = [(2010, "Steve Martin"),
               (2009, "Hugh Jackman"),
               (2008, "Jon Stewart"),
               (2007, "Ellen DeGeneres"),
               (2006, "Jon Stewart"),
               (2005, "Chris Rock"),
               (2004, "Billy Crystal"),
               (2003, "Steve Martin"),
               (2002, "Whoopi Goldberg"),
               (2001, "Steve Martin"),
               (2000, "Billy Crystal"),
            ]
```


```python
create_ceremonies = "CREATE TABLE ceremonies (id integer PRIMARY KEY,Year integer,Host text);"
conn.execute(create_ceremonies)



```




    OperationalErrorTraceback (most recent call last)

    <ipython-input-6-9cde5619bf5a> in <module>()
          1 create_ceremonies = "CREATE TABLE ceremonies (id integer PRIMARY KEY,Year integer,Host text);"
    ----> 2 conn.execute(create_ceremonies)
          3
          4


    OperationalError: table ceremonies already exists



```python
insert_query = "INSERT INTO ceremonies (Year, Host) VALUES (?,?);"
conn.executemany(insert_query, years_hosts)
```


```python

print(conn.execute("select * from ceremonies limit 10;").fetchall())
print(conn.execute("pragma table_info(ceremonies);").fetchall())
```

# Foreign Key Constraints


```python
q_keys_on = "PRAGMA foreign_keys = ON;"
conn.execute(q_keys_on)
```

# Setting Up One-To-Many


```python
# Lets create the nominations_two table

q_create_nom_2 = '''CREATE TABLE nomination_two(
id integer PRIMERY KEY,
category text,
nominee text,
movie text,
character text,
won text,
ceremony_id integer,
FOREIGN KEY(ceremony_id) REFERENCES ceremonies(id)
);'''

nom_query = '''
select ceremonies.id as ceremony_id, nominations.category as category,
nominations.nominee as nominee, nominations.movie as movie,
nominations.character as character, nominations.won as won
from nominations
inner join ceremonies
on nominations.year == ceremonies.year
;
'''

joined_nominations = conn.execute(nom_query).fetchall()

conn.execute(q_create_nom_2)
```




    OperationalErrorTraceback (most recent call last)

    <ipython-input-14-98e7efc5b2ba> in <module>()
         24 joined_nominations = conn.execute(nom_query).fetchall()
         25
    ---> 26 conn.execute(q_create_nom_2)


    OperationalError: table nomination_two already exists



```python
insert_nominations_two = '''insert into nomination_two (ceremony_id, category, nominee, movie, character, won)
values (?,?,?,?,?,?);
'''

conn.executemany(insert_nominations_two, joined_nominations)
print(conn.execute("select * from nomination_two limit 5;").fetchall())
```

    [(None, 'Actor -- Leading Role', 'Javier Bardem', 'Biutiful', 'Uxbal', '0', 1), (None, 'Actor -- Leading Role', 'Jeff Bridges', 'True Grit', 'Rooster Cogburn', '0', 1), (None, 'Actor -- Leading Role', 'Jesse Eisenberg', 'The Social Network', 'Mark Zuckerberg', '0', 1), (None, 'Actor -- Leading Role', 'Colin Firth', "The King's Speech", 'King George VI', '1', 1), (None, 'Actor -- Leading Role', 'James Franco', '127 Hours', 'Aron Ralston', '0', 1)]


# Deleting And Renaming Tables


```python
delete_nom ="DROP TABLE nominations;"
conn.execute(delete_nom)
```




    <sqlite3.Cursor at 0x7fd32899c810>




```python
rename_nom = "ALTER TABLE nomination_two RENAME TO nominations;"
conn.execute(rename_nom)
```




    <sqlite3.Cursor at 0x7fd32899cea0>



# Creating A Join Table


```python
create_movies = "create table movies (id integer primary key,movie text);"
create_actors = "create table actors (id integer primary key,actor text);"
create_movies_actors = '''create table movies_actors (id INTEGER PRIMARY KEY,
movie_id INTEGER, actor_id INTEGER,
FOREIGN KEY(movie_id) references movies(id),
FOREIGN KEY(actor_id) references actors(id));
'''
conn.execute(create_movies)
conn.execute(create_actors)
conn.execute(create_movies_actors)
```




    OperationalErrorTraceback (most recent call last)

    <ipython-input-39-a3f61fdfe730> in <module>()
          6 FOREIGN KEY(actor_id) references actors(id));
          7 '''
    ----> 8 conn.execute(create_movies)
          9 conn.execute(create_actors)
         10 conn.execute(create_movies_actors)


    OperationalError: table movies already exists



```python
print(conn.execute("select * from actors limit 5").fetchall())
```

    [(1, 'Javier Bardem'), (2, 'Jeff Bridges'), (3, 'Jesse Eisenberg'), (4, 'Colin Firth'), (5, 'James Franco')]



```python
insert_movies = "insert into movies (movie) select distinct movie from nominations;"
insert_actors = "insert into actors (actor) select distinct nominee from nominations;"
conn.execute(insert_movies)
conn.execute(insert_actors)

print(conn.execute("select * from movies limit 5;").fetchall())
print(conn.execute("select * from actors limit 5;").fetchall())
```

    [(1, 'Biutiful'), (2, 'True Grit'), (3, 'The Social Network'), (4, "The King's Speech"), (5, '127 Hours')]
    [(1, 'Javier Bardem'), (2, 'Jeff Bridges'), (3, 'Jesse Eisenberg'), (4, 'Colin Firth'), (5, 'James Franco')]
