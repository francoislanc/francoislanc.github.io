+++
title = "Exploring movies data in a triplestore 🎥"
description = ""
tags = [
    "data",
    "movie",
    "triplestore",
    "query"
]
date = "2021-01-03"
+++

Let's explore a [dataset](https://www.kaggle.com/shivamb/netflix-shows) from Flixable, which is a third-party Netflix search engine and IMDb and try to answer the following questions:

1. [What are the top movies on Netflix according to the IMDb rating?](./#query1)
2. [What are the top countries producing films?](./#query2)
3. [Who are the cast members who appear in the most Netflix Movies?](./#query3)
4. [What are the top movies added on Netflix between May 2018 and August 2018?](./#query4)
5. [What is the last movie from Steven Spielberg added on Netflix?](./#query5)

The initial data are stored in a csv:
[![Initial csv data](/exploring_movies_data_in_a_triplestore/movies_data_raw_csv.png)](/exploring_movies_data_in_a_triplestore/movies_data_raw_csv.png)



After cleaning and transformation, the data are loaded into a triplestore for querying:
[![Data in a triplestore](/exploring_movies_data_in_a_triplestore/movies_data_triplestore.png)](/exploring_movies_data_in_a_triplestore/movies_data_triplestore.png)

Then the questions are transformed into SPARQL-like queries and run against the triplestore:

## 1. What are the top movies on Netflix according to the IMDb rating? {#query1} 

Query:
```
SELECT ?movie, ?rating
FROM ?g
WHERE {
    ?movie "average_rating"@[] ?rating .
    ?movie "num_votes"@[] ?votes
}
ORDER BY ?rating DESC
HAVING ?votes > "5000"^^type:int64
LIMIT "10"^^type:int64;
```
Output:
```
?movie  ?rating
/movie<schindlers list> "8.9"^^type:float64
/movie<pulp fiction>    "8.9"^^type:float64
/movie<the lord of the rings the return of the king>    "8.9"^^type:float64
/movie<inception>       "8.8"^^type:float64
/movie<the lord of the rings the two towers>    "8.7"^^type:float64
/movie<the matrix>      "8.7"^^type:float64
/movie<city of god>     "8.6"^^type:float64
/movie<once upon a time in the west>    "8.5"^^type:float64
/movie<the departed>    "8.5"^^type:float64
/movie<senna>   "8.5"^^type:float64

[OK] 10 rows retrieved. BQL time: 80.1355ms. Display time: 50.3µs
```

## 2. What are the top countries producing the films? {#query2}

Query:
```
SELECT ?country, COUNT(?movie) AS ?movies_count
FROM ?g
WHERE {
    ?movie "country"@[] ?country
}
GROUP BY ?country
ORDER BY ?movies_count DESC
LIMIT "10"^^type:int64;
```
Output:
```
?country        ?movies_count
"United States"^^type:text      "1304"^^type:int64
"India"^^type:text      "583"^^type:int64
"United Kingdom"^^type:text     "277"^^type:int64
"France"^^type:text     "151"^^type:int64
"Canada"^^type:text     "146"^^type:int64
"Germany"^^type:text    "103"^^type:int64
"Spain"^^type:text      "92"^^type:int64
"China"^^type:text      "76"^^type:int64
"Hong Kong"^^type:text  "76"^^type:int64
"Australia"^^type:text  "57"^^type:int64

[OK] 10 rows retrieved. BQL time: 30.8864ms. Display time: 43.1µs
```

## 3. Who are the cast members who appear in the most Netflix Movies? {#query3}

Query:
```
SELECT ?person, COUNT(?movie) AS ?movies_count
FROM ?g
WHERE {
    ?person "played"@[] ?movie
}
GROUP BY ?person
ORDER BY ?movies_count DESC
LIMIT "10"^^type:int64;
```
Output:
```
?person ?movies_count
/person<Shah Rukh Khan> "23"^^type:int64
/person<Boman Irani>    "22"^^type:int64
/person<Akshay Kumar>   "21"^^type:int64
/person<Paresh Rawal>   "20"^^type:int64
/person<Anupam Kher>    "19"^^type:int64
/person<Naseeruddin Shah>       "18"^^type:int64
/person<Om Puri>        "17"^^type:int64
/person<Nicolas Cage>   "16"^^type:int64
/person<Gulshan Grover> "15"^^type:int64
/person<Kay Kay Menon>  "15"^^type:int64

[OK] 10 rows retrieved. BQL time: 229.6949ms. Display time: 48.9µs
```

## 4. What are the top movies added on Netflix between May 2018 and August 2018? {#query4}

Query:
```
SELECT ?movie, ?time, ?rating
FROM ?g
WHERE {
    /platform<Netflix> "added"@[?time] ?movie .
    ?movie "average_rating"@[] ?rating .
    ?movie "num_votes"@[] ?votes
}
ORDER BY ?rating DESC
HAVING ?votes > "5000"^^type:int64
BETWEEN 2018-05-01T00:00:00Z, 2018-08-31T00:00:00Z
LIMIT "10"^^type:int64;
```
Output:
```
?movie  ?time   ?rating
/movie<rang de basanti> 2018-08-02T00:00:00Z    "8.2"^^type:float64
/movie<andaz apna apna> 2018-05-16T00:00:00Z    "8.2"^^type:float64
/movie<room>    2018-07-19T00:00:00Z    "8.1"^^type:float64
/movie<haider>  2018-08-02T00:00:00Z    "8.1"^^type:float64
/movie<inequality for all>      2018-08-29T00:00:00Z    "8"^^type:float64
/movie<her>     2018-07-29T00:00:00Z    "8"^^type:float64
/movie<the kings speech>        2018-06-02T00:00:00Z    "8"^^type:float64
/movie<thor ragnarok>   2018-06-05T00:00:00Z    "7.9"^^type:float64
/movie<pad man> 2018-08-21T00:00:00Z    "7.9"^^type:float64
/movie<amy>     2018-07-26T00:00:00Z    "7.8"^^type:float64

[OK] 10 rows retrieved. BQL time: 10.38ms. Display time: 58µs
```

## 5. What is the last movie from Steven Spielberg added on Netflix? {#query5}

Query:
```
SELECT ?movie, ?time
FROM ?g
WHERE {
    /platform<Netflix> "added"@[?time] ?movie .
    /person<Steven Spielberg> "directed"@[] ?movie
}
ORDER BY ?time DESC
LIMIT "1"^^type:int64;
```
Output:
```
?movie  ?time
/movie<catch me if you can>     2020-01-01T00:00:00Z

[OK] 1 rows retrieved. BQL time: 18.1343ms. Display time: 35.1µs
```


Developed with [Badwolf](http://google.github.io/badwolf/) triplestore and [G6](https://g6.antv.vision/en) graph visualization engine.  
The source code is available on [Github](https://github.com/francoislanc/exploring-movies-data-in-a-triplestore).
