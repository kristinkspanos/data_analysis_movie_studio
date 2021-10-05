# Movie Studio Analysis

## project goals
Use data analysis to help a film studio determine what leads to a successful movie. This project was developed by Numa Dhamani as part of my mentorship.

## results
See findings_blog_post.md for summary of results.

## built with
* Python 3
* Jupyter Notebook

## data sources
[IMDB 5000 movie dataset](https://www.kaggle.com/carolzhangdc/imdb-5000-movie-dataset)

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
