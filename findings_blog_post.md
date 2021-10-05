# Movie Studio Analysis Findings
## Scenario
After a few tough years financially and a series of unsuccessful films, a movie studio is looking to update their strategy. I analyzed a dataset of over 5000 films with the goal of developing insights on what elements contribute to a successful film.

## Investigate the data through exploratory data analysis 
Before diving into the analysis, I performed exploratory data analysis (EDA) to familiarize myself with the variables included in the dataset. 

The variables can be divided into five categories: 
*	Identifiers
*	Inputs (metrics that the movie studio can influence) 
*	Non-financial metrics that represent the popularity of the actors and directors in a movie 
*	Non-financial metrics of a movie’s success 
*	Financial metrics of a movie’s success 

### Identifiers: 
*	movie_title 
*	title_year 
 
### Numeric variables: 
Inputs (metrics that the movie studio can influence) 
*	duration 
*	aspect_ratio 
*	budget
*	budget_millions (calculated field)

Non-financial metrics (represent the popularity of the actors and directors in a movie)
*	director_facebook_likes 
*	actor_1_facebook_likes 
*	actor_2_facebook_likes 
*	actor_3_facebook_likes 
*	cast_total_facebook_likes 
*	movie_facebook_likes

Non-financial metrics of a movie’s success 
*	num_critic_reviews 
*	num_user_reviews 
*	num_users_voted 
*	movie_score 

Financial metrics of a movie’s success 
*	gross 
*	gross_millions (calculated field)
*	profit_millions (calculated field)
*	roi (calculated field)
*	profit_margin (calculated field)

### Categorical variables 
Inputs (metrics that the movie studio can influence) 
*	color 
*	genres 
*	actor_1_name 
*	actor_2_name 
*	actor_3_name 
*	plot_keywords 
*	language 
*	country 
*	content_rating 

I transformed the ```budget``` and ```gross``` to be shown in millions so they will be easier to interpret. I also added additional variables – ```profit_millions``` (```gross_millions```-```budget_millions```), ```roi```(```profit_millions```/```budget_millions```), and ```profit_margin``` (```profit_millions```/```gross_millions```) - to evaluate the financial results of each movie.

Next, I filtered the dataset to show only the movies that are most relevant to the analysis. The filtered dataset contains only English language movies, and movies released after 1996 (to show 20 years’ worth of data). 

Next step in EDA is to explore the summary statistics and distributions of the numeric variables, as well as relationships between these variables. For this portion of the analysis, I first trimmed the outliers so I could more easily see the distribution of the variables using visualization tools, and then looked at boxplots for each variable. I used the trimmed values to create a heatmap that shows relationships between the variables without the influence of outliers. I also used ```.value_counts()``` to look at the distribution of each categorical variable. 

## Analysis
After exploring the data through EDA, I decided to focus on 4 inputs, and two determinants of success:
*	Inputs
    *	actors (```actor_1_name```, ```actor_2_name```, ```actor_3_name```) 
    *	directors (```director_name```)
    *	genres (```genres```)
    *	plot keywords (```plot_keywords```)
*	Determinants of success
    *	profit (```profit_millions```)
    *	roi (```roi```)

I chose to ignore the non-monetary metrics that represent the popularity of a movie's actors and director (the Facebook likes of the actors and director) because they have weak or non-existent correlations with the monetary metrics of a movie’s success. Moreover, Facebook didn’t exist for the entire period of time we are analyzing, and the audencies that use Facebook and its various features has changed dramatically over the past 15 years.

I assume that the financial metrics of a movie’s success are most relevant to the movie studio’s decision-making processes, and therefore will not consider the non-monetary metrics of a movie’s success in the analysis.

I chose not to include profit margin because this analysis asks me to identify which elements lead to successful movies - not cost-cutting or pricing strategies which might be better captured by profit margin. Moreover, profit margin is highly correlated with ROI, so movies with strong profit margins will likely be captured in ROI analysis.

It's also important to note that we do not have data on the dollar amount paid to each actor or director for appearing in/directing a movie. The profit and ROI figures analyzed capture the profit and ROI of the movie itself. Therefore, we cannot make a judgement on whether a particular actor or director has a strong ROI for his or her salary, but instead whether they appeared in movies that achieved a strong ROI on the movie’s overall budget.

## Actor analysis 
Do certain actors tend to appear in more successful movies? 

The movie_studio dataset has three fields that contain actor names" ```actor_1_name```, ```actor_2_name```, ```actor_3_name```. 

I analyze the outcomes for the lead actor in a movie (```actor_1_name```) separately from the outcomes for the supporting actors (```actor_2_name```, ```actor_3_name```). This method is imperfect, because some movies have more than one headliner, and some have ensemble casts - these realities are not reflected in the data we have available. Therefore, the resulting lists of lead actors with strong financial outcomes may leave out some actors who were not coded as actor_1_name in the movies they starred in. However, this analysis will provide a strong starting point for identifying which actors appear in movies with the strongest financial outcomes.

The list of lead actors is filtered to only show actors who have been lead actor in at least 4 movies. The list of supporting actors is filtered to only show actors who have been a supporting actor in at least 4 movies. 

The first metric analyzed is profit. I normalized the profit metric by dividing each actor’s average profit by the overall average profit. This shows the profit metric’s percent difference from the mean value. 

There are 48 lead actors - including Robert Pattinson, Bryce Dallas Howard, and Steve Carell - and 205 supporting actors - including Seth MacFarlane, Kristen Stewart, and Anna Kendrick - with an average normalized profit greater than two - indicating that the movies these actors appear in have an average profit that is at least twice the overall average (a value of one is an average value).

***Top Experienced Lead Actors by Normalized Avg. Profit***
| ```actor_1_name```  | ```avg_profit_millions``` | ```normalized_profit``` |
| ------------- | ------------- | ------------- |
| Robert Pattinson | 130.8 | 12.8 |
| Bryce Dallas Howard | 128.6 | 12.6 |
| Steve Carell | 97.3| 9.5 |
| Jennifer Lawrence | 84.7 | 8.3 |
| Bradley Cooper | 80.7 | 7.9 |

Next, I analyzed each actor’s ROI. Again, I normalized ROI by dividing each actor’s average ROI by the overall average ROI, creating a metric that shows each profit metric’s percent difference from the mean value. 

There are 31 lead actors and 105 supporting actors with an average normalized ROI, as a pct. of overall average greater than 1.5 - indicating that the movies these actors appear in have an average ROI that is at least 50%.

**Recommendation**
The lead and supporting actors with average normalized profit greater than 2 and/or average normalized ROI greater than 1.5 have a track record of appearing in movies with strong financial results, and should be hired on future movies.

*Further analysis - what is the overlap between these two lists?*

Finally, I looked at summary outcomes by actor, in order to explore if filtering the results of the normalized profit and ROI analysis by actors who have appeared in at least 4 movies left out any highly profitable actors. This analysis revealed that 86% of the lead actors with the highest average profit and 95% of the actors with the highest average ROI have indeed appeared in less than 4 movies, and therefore won’t appear in the previous analysis.

***Top Actors by Avg. Profit***
| ```actor_1_name```  | ```avg_profit_millions``` | ```num_movies``` |
| ------------- | ------------- | ------------- |
| Rupert Everett | 286.5  | 1 |
| CCH Pounder  | 253.7 | 2 |
| Catherine Dyer  | 227 | 1 |

***Top Actors by Avg. ROI***
| ```actor_1_name```  | ```avg_roi``` | ```num_movies``` |
| ------------- | ------------- | ------------- |
| Micah Sloat | 7193  | 1 |
| Greg Ayres | 2959 | 1 |
| Heather Donahue  | 2341 | 1 |

**Recommendation**
The studio should aim to work with the actors identified in the previous analysis to seek out consistent results, it's also important to identify and foster relationships with up-and-coming actors. 

The studio should consider gathering additional data on actors who have appeared in fewer than 4 movies to see if any trends can be identified. The studio may also consider developing programs to identify promising young actors.

## Director analysis 
Do certain directors direct in more successful movies? 

The list of directors is filtered to only show actors who have directed (‘director_name’) at least 4 movies. Again, I analyzed normalized profit and normalized ROI per director.
 
There are 77 directors with an average normalized profit greater than two - including Peter Jackson, Christopher Nolan, and Jon Favreau - indicating that these movies have an average profit that is at least twice the overall average. There are only four directors with average normalized ROI average greater than 1.5 - indicating that the movies these directors direct have an average ROI that is at least 50% above the overall average.

***Top Experienced Directors by Normalized Avg. Profit***
| ```director_name```  | ```avg_profit_millions``` | ```normalized_profit``` |
| ------------- | ------------- | ------------- |
| Peter Jackson | 152 | 14.9 |
| Francis Lawrence | 151.1 | 14.8 |
| Andrew Adamson | 130.6 | 12.8 |
| Phil Lord | 115.2 | 11.3 |
| Christopher Nolan | 101 | 9.9 |

*Further analysis – pick a lower ROI threshold for directors?*
 
**Recommendation**
The directors with average normalized profit greater than 2 and/or average normalized ROI greater than 1.5 have a track record of directing in movies with strong financial results, and should be hired on future movies. 

*Further analysis - what is the overlap between these two lists?*

I also looked at the summary outcomes for all directors for these metrics. This analysis revealed that 75% of the directors with the highest average profit and 21% of the directors with the highest average ROI have appeared in less than 4 movies, and therefore won’t appear in the previous analysis.

**Recommendation**
While the studio should aim to work with directors with a track record of financial success to seek out consistent profit, the most profitable directors, and those whose movies have the highest ROIs, can often be up-and-coming directors. The studio should look for opportunities to engage with aspiring directors.

Further analysis is needed to determine determinants of success for up-and-coming directors. 

## Genre analysis 
How do financial outcomes differ by genre? Which genres are most successful? 
 
Movies can be classified under more than one genre. For this analysis, a movie’s outcomes are included in the aggregate outcome for each genre it is classified as. For example - a movie whose genres are "romance" and "comedy" will be included in the analyses for both genres.

**Average Gross by Genre**
![avg_gross_genre](https://github.com/kristinkspanos/data_analysis_movie_studio/blob/main/genre_avg_gross.png)

Adventure, Animation, Family, Fantasy and Sci-fi movies are the highest grossing, on average.

**Total Gross by Genre**
![total_gross_genre](https://github.com/kristinkspanos/data_analysis_movie_studio/blob/main/genre_sum_gross.png)

The Adventure, Family, Fantasy, and Sci-fi genres have high total gross, in addition to their high average gross. This indicates high volume - each of these genres represent 4.3% - 6.3% of all movies. Despite high average gross, Animation had low total gross due to the fact that only 2% of movies are Animations.

**Average Profit by Genre**
![avg_profit_genre](https://github.com/kristinkspanos/data_analysis_movie_studio/blob/main/genre_avg_profit.png)

Animation and Family have the highest average profits. Adventure, Comedy, Fantasy, Horror, Music, and Sci-fi movies also have above-average average profits. Action, Crime, Documentary, Drama, and Thriller movies tend have below-average profits.

**Total Profit by Genre**
![total_profit_genre](https://github.com/kristinkspanos/data_analysis_movie_studio/blob/main/genre_sum_profit.png)
 
Comedies have the highest total profits. The Comedy genre is high volumne (15% of all movies) and Comedies have have above-average profitability.
 
**Recommendation**
Focus on growth in two categories:
*	Blockbusters (high margin, low volume)
  *	Genres: Action, Adventure, and Fantasy movies
  *	Budget: High-budget
  *	Frequency: low frequency
*	Crowd-pleasers (low margin, high volume)
  *	Genres: Romance, Comedy, Animation, Family
  *	Budget: low-budget
  *	Frequency: high frequency

De-emphasize less profitable genres - including Action, Crime, Thriller, and Drama.

## Keyword analysis 
Do movies with certain plot keywords have more successful outcomes? 
 
More than one plot keyword may be associated with a movie. For this analysis, a movie’s outcomes are included in the aggregate outcome for each plot keyword associated with that movie. For example - a movie whose plot keywords are "doctor" and "scientist" will be included in the analyses for both keywords. 
 
The list of movies is filtered to only show keywords (‘plot_keywords’) associated with at least 30 movies.

There are only 6 keywords with average normalized profit greater than 2, and none with average normalized ROI greater than 1.5. This indicates that there is likely large variation in the outcomes for any given keyword. Because the normalized profit and ROI analysis did not produce many keywords of interest, we will instead look at the highest grossing and most profitable keywords.
Highest grossing and most profitable keywords:
*	Movies with the plot keywords 'sequel', 'battle', 'spy', 'alien', and 'island' are the highest grossing, on average.
*	Movies with the plot keywords 'wedding', 'island', 'high school', 'female nudity', and 'hospital' are the most profitable, on average.
*	Movies with the plot keywords 'small town', 'writer', 'escape', 'scientist', 'boy', 'future', and 'box office flop' are not profitable, on average.

**Recommendation**
The plot keywords with the highest average gross and profit are likely to be associated with financially successful films. Future films should consider these plot themes.

## Conclusion
The analysis identified groups of lead actors, supporting actors, and directors whose movies are financially successful, on average. I also recommended that the studio focus on two genre groupings - blockbusters (high margin, low volume films), and crowd-pleasers (low margin, high-volume films – and deemphasize less profitable genres. Finally, I identified keywords that have high average profit and ROI – as well as keywords with weak results. These keywords provide direction for which plot themes the studio should embrace and avoid in the future.

Recommendations:
* Lead and Supporting Actors
  * The analysis identified lead and supporting actors with a history of strong financial outcomes. These actors should be considered for future projects.
  * I also discovered that most of the top actors by profit and ROI are inexperienced. Therefore, the studio should collect and analyze data to try and identify the determinants of success for inexperienced actors. Potential data points include: experience acting in non-movie projects (such as TV shows, theatre productions, or comedy shows), and financial and popular success of non-movie projects.
* Directors
  * I identified directors with a history of strong financial outcomes. These directors should be considered for future projects.
  * Similar to the results for actors, I also found that many top directors by average profit and ROI are inexperienced. The studio should look for opportunities to connect with up-and-coming directors, as well as identify the determinants of success for inexperienced directors. Potential data points include: experience directing non-movie projects (such as TV shows or music videos), experience working as a producer, writer, camera operator, or in another production-oriented role on a movie or non-movie projects. 
* Genres - focus on growth in two categories:
  *	Blockbusters (high margin, low volume)
    *	Genres: Action, Adventure, and Fantasy movies
    *	Budget: High-budget
    *	Frequency: low frequency
  *	Crowd-pleasers (low margin, high volume)
    *	Genres: Romance, Comedy, Animation, Family
    *	Budget: low-budget
    *	Frequency: high frequency
* Plot keywords
  * I identified the plot keywords with the highest average gross and profit, as well as the keywords that are unprofitable, on average. The studio should aim to develop films that follow one or more of these plot themes. 

 ## Ideas for Additional Analysis
 
This is not an exhaustive analysis of all the elements that could contribute to the financial success of a movie. Additional analysis could be performed on the data in the dataset provided:
*	How successful are sequels and series'?
*	Closer look at popular groupings of genres (i.e. romance and comedy; action and adventure).
*	Closer look at popular groupings of keywords.
*	Group similar keywords together. (i.e. ‘marriage’, ‘marriage ceremony’, and ‘marriage proposal’ are all separate keywords – but it may be useful to analyze their results together. 
* Analysis of outcomes by content rating.

While this analysis focuses on increasing revenue for the movie studio, the studio could also explore strategies for cutting costs using more detailed budget data. Moreover, the studio could explore distribution strategies using data on revenue sources (movie theatres, streaming services, television replays, etc.).

