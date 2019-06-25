---
layout: project
type: project
image: images/pley_icon.png
title: Exploring a Data Scrape
permalink: projects/yelpDB-Flask-SQLite
# All dates must be YYYY-MM-DD format!
date: 2019-04-09
labels:
  - Python
  - Flask
  - SQLite
  - GitHub
summary: A database was formed using data scraped from Yelp. This project is a web page that explores the database and displays the results. 
---

<img class="ui medium right floated rounded image" src="../images/pleywindow.png"> 

This is a project utilizing Flask and SQLite to allow us to search a database using Python. [Flask](http://flask.pocoo.org/), is a microframework used for local server. [SQLite](https://www.sqlite.org/index.html) is the library used to issue queries to the database.

The web page displays adjustable search criteria and issues a request for the corresponding data from the database. The results are displayed on a secondary web page. 

The database contains around 100 restaurant records scraped from Yelp.

Here is an example of how queries are issued to the database based upon the given criteria:

<img class="ui medium right floated rounded image" src="../images/pleyresult.png">

```python
def response():
    minRating=request.form["minRating"]
    category=request.form["category"]
    sorting=request.form["sorting"]
    if sorting=='rating':
        sortstring='rating DESC'
    elif sorting=='neighborhood':
        sortstring='neighborhood'
    else:
        sortstring='rating DESC, neighborhood ASC'
    db = get_db()
    cursor = db.cursor()
    dataList=cursor.execute("select * from company where rating>="+minRating+" and category like '%"+category+"%' order by "+sortstring).fetchall()
    return render_template('results_page.html',data=dataList)
```

Source: <a href="https://github.com/mikepando/yelpDB-Flask-SQLite"><i class="large github icon "></i>mikepando/yelpDB-Flask-SQLite</a>
