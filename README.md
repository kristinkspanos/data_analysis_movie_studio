# Movie Studio Analysis

## project goals
After a few tough years financially and a series of unsuccessful films, a movie studio is looking to update their strategy. I analyzed a dataset of over 5000 films with the goal of developing insights on what elements contribute to a successful film.

## recommendations
I analyzed the relationships between financial outcomes and several factors that the studio may consider when planning their films: lead actors, supporting actors, directors, genres, and plot themes.

## results
See findings_blog_post.md for summary of results.

## built with
* Python 3
* Jupyter Notebook
* Matplotlib
* Scipy

## data sources
[IMDB 5000 Movie Dataset](https://www.kaggle.com/carolzhangdc/imdb-5000-movie-dataset)

### Numeric Variables
Field | Description
------------ | -------------
num_critic_reviews| number of critic
duration | duration (minutes)
director_facebook_likes| number of facebook likes, movie director 
actor_1_facebook_likes| number of facebook likes, headline actor
actor_2_facebook_likes| number of facebook likes, supporting actor 1
actor_3_facebook_likes| number of facebook likes, supporting actor 2
movie_facebook_likes| number of facebook likes, movie
cast_total_facebook_likes (int)| number of facebook likes, cast (int)
gross| gross income
budget| budget
movie_score| movie rating (possible values are between 1 and 10)
num_users_voted | unknown; we assume ths refers to the number of users who voted on a movie's rating
num_user_reviews| unknown; we assume this refers to the number of users who left a review for the movie
aspect_ratio | aspect ratio (int)

### Categorical Variables
Field | Description
------------ | -------------
color| color or black and white (binary)
director_name| name of director
actor_1_name| name of headline actor
actor_2_name| name of supporting actor 1
actor_3_name| name of support actor 2
title_year| year of release
genres| movie genres
plot_keywords| plot keywords
language| language
country| country
content_rating| content rating (PG, PG13, etc.)

## acknowledgements
The project prompt and dataset were provided by Numa Dhamani as part of my mentorship.
