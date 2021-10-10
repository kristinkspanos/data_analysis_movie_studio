# Movie Studio Analysis

## Project Goals
I analyzed a dataset of over 5000 films with the goals of developing insights on what features contribute to a successful film and providing recommendations to a movie studio looking to update their strategy.

I tried to answer the following questions:
* Which lead and supporting actors tend to appear in movies with strong financial outcomes? Can I identify a list of actors with a track record of successful films for the studio to consider when planning future projects?
* Which directors direct the most financially successful films? Can I produce a list of directors with a history of strong financial outcomes for the studio to use when planning future projects?
* Which genres have the strongest financial outcomes - including the highest average profit and gross revenue, and the highest total profit and revenue? Which genres should the studio focus on in the future, and which genres should the studio de-emphasize?
* Which plot themes are associated with financial success? Which themes tend to be associated with unsuccessful movies? 

For a full explanation of my analysis, please see [Movie Studio Analysis Findings](https://github.com/kristinkspanos/data_analysis_movie_studio/blob/main/findings_blog_post.md)

## Recommendations
I analyzed the relationships between financial outcomes and several factors that the studio may consider when planning their films: lead actors, supporting actors, directors, genres, and plot themes.

### Lead and Supporting Actors
* The analysis identified experienced (appeared in 4 or more movies) lead and supporting actors with a history of strong financial outcomes. These actors should be considered for future projects.
  * Top lead actors by average profit include: Robert Pattinson, Bryce Dallas Howard, Steve Carell, Jennifer Lawrence, Bradley Cooper
  * Top supporting actors by average profit include: Billy Boyd, Josh Hutcherson, Joel David Moore, Rupert Grint, and John Ratzenberger
  * Top lead actors by ROI include: Mark Margolis, Lin Shaye, Noel Gugliemi, Robert Duvall, and Kevin Zegers
  * Top supporting actors by ROI include: Jon Gries, Barbara Hershey, Diedrich Bader, Shawnee Smith, and Ethan Suplee
* I also discovered that most of the top actors by profit and ROI are inexperienced (defined as appearing in fewer than 4 movies). The studio should collect and analyze data to try and identify the determinants of success for inexperienced actors. Potential data points include: 
  * Experience acting in non-movie projects (such as TV shows, theatre productions, or comedy shows)
  * Financial and popular success of non-movie projects

### Directors
 * I identified experienced directors (directed 4 or more movies) with a history of strong financial outcomes. These directors should be considered for future projects.
   * Top directors by average profit include: Peter Jackson, Francis Lawrence, Andrew Adamson, Phil Lord, and Christopher Nolan
   * Top directors by ROI include: Alex Kendrick, James Wan, Darren Aronofsky, Michael Moore, and Darren Lynn Bousman
* Similar to the results for actors, I also found that many top directors by average profit and ROI are inexperienced (directed fewer than 4 movies). The studio should look for opportunities to connect with up-and-coming directors, as well as identify the determinants of success for inexperienced directors. Potential data points include:
  *  Experience directing non-movie projects (such as TV shows or music videos)
  *  Experience working as a producer, writer, camera operator, or in another production-oriented role on a movie or non-movie projects

### Genres
* Focus on growth in two categories - blockbusters and crowd-pleasers:
  *	Blockbusters
    *	high margin, low volume
    *	genres: adventure, sci-fi, and fantasy movies
  *	Crowd-pleasers
    * low margin, high volume	 
    *	genres: romance, comedy, animation, and family movies
 * De-emphasize	less profitable genres, including action, crime, thriller, and drama

### Plot Keywords
* The studio should aim to develop films that follow one or more of the plot themes that tend to be associated with profitable films, and avoid plot keywords that tend to be associated with unprofitable films. There appears to be great variation in the results per keyword, so further analysis is needed to determine which keywords are associated with consistent, positive finacial outcomes.
   * Movies with the plot keywords 'wedding', 'island', 'high school', 'female nudity', and 'hospital' are the most profitable, on average.
   * Movies with the plot keywords 'small town', 'writer', 'escape', 'scientist', 'boy', 'future', and 'box office flop' are not profitable, on average.

## Built With
* Python 3
* Jupyter Notebook
* Functools
* Matplotlib
* Numpy
* Scipy

## Data Sources
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
director_name| name of movie director
actor_1_name| name of headline actor
actor_2_name| name of supporting actor 1
actor_3_name| name of support actor 2
title_year| year of release
genres| movie genres
plot_keywords| plot keywords
language| language
country| country
content_rating| content rating (PG, PG13, etc.)

## Acknowledgements
Kristin Kent Spanos

kristinkspanos@gmail.com
