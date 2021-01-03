+++
title = "Exploring movies data in a triplestore 🎥"
description = ""
tags = [
    "data analytics",
    "movie",
    "triplestore",
    "query"
]
date = "2021-01-03"
+++

Let's explore [a dataset](https://www.kaggle.com/shivamb/netflix-shows) from [Flixable](https://flixable.com/), which is a third-party [Netflix](netflix.com) search engine and [IMDb](https://www.imdb.com/) and try to answer the following questions:

1. What are the top 10 movies on Netflix according to the IMDb rating?
2. What are the countries producing the 100 most popular films?
3. What are the top genres of the 100 most popular films?
4. Who are the top 10 cast members who appear in the most Netflix Movies?
5. What is the best movie added on Netflix between May 2018 and August 2018?
6. What is the latest movie from Steven Spielberg added on Netflix?

The initial data are stored in a csv :
![Initial data](/exploring_movies_data_in_a_triplestore/movies_data_raw_csv.png)

After cleaning and transformation, the data are loaded into [a triplestore](http://google.github.io/badwolf/) for querying.

The source code is available on [Github](https://github.com/francoislanc/exploring-movies-data-in-a-triplestore).
