# Movie Studio Analysis Findings
## Scenario
After a few tough years financially and a series of unsuccessful films, a movie studio is looking to update their strategy. I analyzed a dataset of over 5000 films with the goal of developing insights on what elements contribute to a successful film.

Check out the full analysis on [GitHub](https://github.com/kristinkspanos/data_analysis_movie_studio).

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

I used ```.value_counts()``` to look at the distribution of each categorical variable. The next step in EDA is to explore the summary statistics and distributions of the numeric variables, as well as relationships between these variables. For this portion of the analysis, I first trimmed the outliers so I could more easily see the distribution of the variables using visualization tools, and then looked at boxplots for each variable.

***Boxplot - ROI***

![boxplot_roi](https://github.com/kristinkspanos/data_analysis_movie_studio/blob/main/visualizations/boxplot_roi_compare.png)

I used the trimmed values to create a heatmap that shows relationships between the variables without the influence of outliers.

***Heatmap***
![heatmap](https://github.com/kristinkspanos/data_analysis_movie_studio/blob/main/visualizations/heatmap.png)

## Analysis
After exploring the data through EDA, I decided to focus on 4 inputs, and 2 determinants of success:
*	Inputs
    *	actors (```actor_1_name```, ```actor_2_name```, ```actor_3_name```) 
    *	directors (```director_name```)
    *	genres (```genres```)
    *	plot keywords (```plot_keywords```)
*	Determinants of success
    *	profit (```profit_millions```)
    *	roi (```roi```)

Profit is best for analyzing films with the largest overall profit, but when taken on its own, it may mask the success of films that require fewer resources, but achieve strong financial results in relation to those resources. ROI captures profit in relation to budget, and is therefore a good metric for capturing films that use their resources efficiently. 

I chose not to include profit margin because this analysis asks me to identify which elements lead to successful movies - not cost-cutting or pricing strategies which might be better captured by profit margin. Moreover, profit margin is highly correlated with ROI, so movies with strong profit margins will likely be captured in ROI analysis.

I chose to ignore the non-monetary metrics that represent the popularity of a movie's actors and director (the Facebook likes of the actors and director) because they have weak or non-existent correlations with the monetary metrics of a movie’s success. Moreover, Facebook didn’t exist for the entire period of time we are analyzing, and the audencies that use Facebook and its various features has changed dramatically over the past 15 years.

I assume that the financial metrics of a movie’s success are most relevant to the movie studio’s decision-making processes, and therefore will not consider the non-monetary metrics of a movie’s success in the analysis.

It's also important to note that we do not have data on the dollar amount paid to each actor or director for appearing in/directing a movie. The profit and ROI figures analyzed capture the profit and ROI of the movie itself. Therefore, we cannot make a judgement on whether a particular actor or director has a strong ROI for his or her salary, but instead whether they appeared in movies that achieved a strong ROI on the movie’s overall budget.

## Actor analysis 
Do certain actors tend to appear in more successful movies? 

The movie_studio dataset has three fields that contain actor names: ```actor_1_name```, ```actor_2_name```, ```actor_3_name```. 

I analyze the outcomes for the lead actor in a movie (```actor_1_name```) separately from the outcomes for the supporting actors (```actor_2_name```, ```actor_3_name```). This method is imperfect, because some movies have more than one headliner, and some have ensemble casts - these realities are not reflected in the data we have available. Therefore, the resulting lists of lead actors with strong financial outcomes may leave out some actors who were not coded as actor_1_name in the movies they starred in. However, this analysis will provide a strong starting point for identifying which actors appear in movies with the strongest financial outcomes.

The list of lead actors is filtered to only show actors who have been lead actor in at least 4 movies. The list of supporting actors is filtered to only show actors who have been a supporting actor in at least 4 movies. 

The first metric analyzed is profit. I normalized the profit metric by dividing each actor’s average profit by the overall average profit. This shows the profit metric’s percent difference from the mean value. I set the profit baseline (the minimum value to be captured by the analysis) to the 75th percentile of normalized profit for all movies - which is equal to 2.09, or a little bit more than twice the average profit.

There are 48 lead actors - including Robert Pattinson, Bryce Dallas Howard, and Steve Carell - and 128 supporting actors - including Billy Boyd, Josh Hutcherson, and Joel David Moore - with an average normalized profit greater than two - indicating that the movies these actors appear in have an average profit that is at least twice the overall average (a value of one is an average value).

(<div class='tableauPlaceholder' id='viz1633904283179' style='position: relative'><noscript><a href='#'><img alt='Dashboard 1 ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ac&#47;Actorswithhighestaverageprofitpermovie&#47;Dashboard1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Actorswithhighestaverageprofitpermovie&#47;Dashboard1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ac&#47;Actorswithhighestaverageprofitpermovie&#47;Dashboard1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1633904283179');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else { vizElement.style.width='100%';vizElement.style.height='727px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>)

***Top Experienced Lead Actors by Normalized Avg. Profit***
| ```actor_1_name```  | ```avg_profit_millions``` | ```normalized_profit``` |
| ------------- | ------------- | ------------- |
| Robert Pattinson | 130.8 | 12.8 |
| Bryce Dallas Howard | 128.6 | 12.6 |
| Steve Carell | 97.3| 9.5 |
| Jennifer Lawrence | 84.7 | 8.3 |
| Bradley Cooper | 80.7 | 7.9 |

***Top Experienced Supporting Actors by Normalized Avg. Profit***
| ```names```  | ```avg_profit_millions``` | ```normalized_profit``` |
| ------------- | ------------- | ------------- |
| Billy Boyd | 188.8 | 18.5 |
| Josh Hutcherson | 184.3 | 18.1 |
| Joel David Moore | 176.2 | 17.3 |
| Rupert Grint | 118.3 | 11.6 |
| John Ratzenberger | 116.2 | 11.4 |

Four of top five supporting actors by normalized average profit all appeared in blockbuster series' (Billy Boyd in Lord of the Rings, Josh Hutcherson in Hunger Games, Rupert Grint in Harry Potter, and Josh Ratzenberger in Toy Story, Monsters Inc., Cars, and The Incredibles). It's unclear what the impact of series' are on an actor's career - do actors who appear in blockbuster series have strong financial outcomes in subsequent films? Or are they unable to break the mold of the character they repeatedly played? This is an interesting question for further analysis.

Next, I analyzed each actor’s ROI. I set the baseline ROI at the 75th percentile of ROI for all movies - which equals and ROI of 94%.

There are 54 lead actors - including Mark Margolis, Lin Shaye, and Noel Gugliemi -  and 113 supporting actors - including John Gries, Barbara Hershey, and Diedrich Bader - with an average ROI greater than 94%.

***Top Experienced Lead Actors by ROI***
| ```actor_1_name```  | ```roi``` |
| ------------- | ------------- |
| Mark Margolis | 18.8 | 
| Lin Shaye | 16 |
| Noel Gugliemi | 6.3 |
| Robert Duvall | 5 |
| Kevin Zegers | 3.7 |

***Top Experienced Supporting Actors by ROI***
| ```names```  | ```roi``` |
| ------------- | ------------- |
| Jon Gries | 28 | 
| Barbara Hershey | 25.4 |
| Diedrich Bader	 | 18.3 |
| Shawnee Smith | 15.9 |
| Ethan Suplee | 12.6 |

**Recommendation**
The lead and supporting actors with average normalized profit greater than 2.09 and/or average ROI greater than 94% have a track record of appearing in movies with strong financial results, and should be hired on future movies.

There is overlap between lists of lead actors with average normalized profit above the profit baseline, and lead actors with average roi above the roi baseline - between the two lists, there are 72 lead actors. Similarly, there is overlap between the two lists of supporting actors. Between those two lists, there are 175 supporting actors.

Finally, I looked at summary outcomes by actor, in order to explore if filtering the results of the normalized profit and ROI analysis by actors who have appeared in at least 4 movies left out any highly profitable actors. This analysis revealed that 86% of the lead actors with the highest average profit and 95% of the actors with the highest average ROI have indeed appeared in less than 4 movies, and therefore won’t appear in the previous analysis.

***Top Actors by Avg. Profit***
| ```actor_1_name```  | ```avg_profit_millions``` | ```num_movies``` |
| ------------- | ------------- | ------------- |
| Rupert Everett | 286.5  | 1 |
| CCH Pounder  | 253.7 | 2 |
| Catherine Dyer  | 227 | 1 |
| Kathleen Freeman  | 207.7 | 1 |
| Phaldut Sharma  | 174.1 | 1 |

***Top Actors by Avg. ROI***
| ```actor_1_name```  | ```avg_roi``` | ```num_movies``` |
| ------------- | ------------- | ------------- |
| Micah Sloat | 7193  | 2 |
| Greg Ayres | 2959 | 1 |
| Heather Donahue  | 2341 | 1 |
| Pfeider Brown  | 226.6 | 1 |
| Chemeeka Walker  | 176.4 | 4 |

**Recommendation**
The studio should aim to work with the actors identified in the previous analysis to seek out consistent results, it's also important to identify and foster relationships with up-and-coming actors. 

The studio should consider gathering additional data on actors who have appeared in fewer than 4 movies to see if any trends can be identified.  Potential data points include:
* Experience acting in non-movie projects (such as TV shows, theatre productions, or comedy shows)
* Financial and popular success of non-movie projects

## Director analysis 
Do certain directors direct in more successful movies? 

The list of directors is filtered to only show actors who have directed (‘director_name’) at least 4 movies. Again, I analyzed normalized profit and normalized ROI per director.
 
There are 74 directors with an average normalized profit greater than the profit baseline - including Peter Jackson, Francis Lawrence, and Andrew Adamson - indicating that these movies have an average profit that is at least twice the overall average. 

***Top Experienced Directors by Normalized Avg. Profit***
| ```director_name```  | ```avg_profit_millions``` | ```normalized_profit``` |
| ------------- | ------------- | ------------- |
| Peter Jackson | 152 | 14.9 |
| Francis Lawrence | 151.1 | 14.8 |
| Andrew Adamson | 130.6 | 12.8 |
| Phil Lord | 115.2 | 11.3 |
| Christopher Nolan | 101 | 9.9 |

There are 77 directors with average normalized ROI average greater than the ROI baseline - including Alex Kendrick, James Wan, and Darren Aronofsky indicating that the movies these directors direct have an average ROI that is at least 0.94 - or 94%.

***Top Experienced Directors by ROI***
| ```director_name```  | ```roi``` |
| ------------- | ------------- |
| Alex Kendrick | 61 |
| James Wan | 14.8 |
| Darrem Aronofsky | 10.4 |
| Michael Moore | 8.3 |
| Darren Lynn Bousman | 8 |
 
**Recommendation**
The directors with average normalized profit greater than 2 and/or average normalized ROI greater than 1.5 have a track record of directing in movies with strong financial results, and should be hired on future movies. 

There is overlap between lists of directors with average normalized profit above the profit baseline, and directors with average roi above the roi baseline. Between the two lists, there are 105 directors. 

I also looked at the summary outcomes for all directors for these metrics. This analysis revealed that 75% of the directors with the highest average profit and 21% of the directors with the highest average ROI have appeared in less than 4 movies, and therefore won’t appear in the previous analysis.

***Top Direrctors by Avg. Profit***
| ```director_name```  | ```avg_profit_millions``` | ```num_movies``` |
| ------------- | ------------- | ------------- |
| James Cameron | 491.1  | 2 |
| Tim Miller | 305 | 1 |
| George Lucas | 274.2 | 3 |
| Kyle Balda | 262 | 1 |
| Colin Trevorrow | 252.7 | 2 |

***Top Directors by Avg. ROI***
| ```director_name```  | ```avg_roi``` | ```num_movies``` |
| ------------- | ------------- | ------------- |
| Oren Peli | 7193.5  | 1 |
| Jonathan Caouette | 2959 | 1 |
| Daniel Myrick  | 2341 | 1 |
| Travis Cluff  | 226.6 | 1 |
| Alex Kendrick  | 50.97 | 1 |

**Recommendation**
While the studio should aim to work with directors with a track record of financial success in order to seek out consistent profit, the most profitable directors, and those whose movies have the highest ROIs, are can often be up-and-coming directors. Therefore, the studio should not ignore new talent and should gather more data on inexperienced directors. Potential data points include:
* Experience directing non-movie projects (such as TV shows or music videos)
* Experience working as a producer, writer, camera operator, or in another production-oriented role on a movie or non-movie projects

## Genre analysis 
How do financial outcomes differ by genre? Which genres are most successful? 
 
Movies can be classified under more than one genre. For this analysis, a movie’s outcomes are included in the aggregate outcome for each genre it is classified as. For example - a movie whose genres are "romance" and "comedy" will be included in the analyses for both genres.

The Adventure, Family, Fantasy, and Sci-fi genres have high total gross, in addition to their high average gross. This indicates high volume - each of these genres represent 4.3% - 6.3% of all movies. Despite high average gross, Animation had low total gross due to the fact that only 2% of movies are Animations.

**Average Profit by Genre**
![avg_profit_genre](https://github.com/kristinkspanos/data_analysis_movie_studio/blob/main/visualizations/barplot_avg_profit_genre.png)

Animation and Family have the highest average profits. Adventure, Comedy, Fantasy, Horror, Music, and Sci-fi movies also have above-average average profits. Action, Crime, Documentary, Drama, and Thriller movies tend have below-average profits.

**Total Profit by Genre**
![total_profit_genre](https://github.com/kristinkspanos/data_analysis_movie_studio/blob/main/visualizations/barplot_total_profit_genre.png)
 
Comedies have the highest total profits. The Comedy genre is high volumne (15% of all movies) and Comedies have have above-average profitability.
 
**Recommendation**
Focus on growth in three categories:
*	Blockbusters (high margin, low volume) - Blockbusters are high-budget, high-margin films. The resources required to produce these films means that they are released infrequently. Blockbuster genres include Adventure (6.3% of all films), Fantasy (4.3% of all films), Sci-fi movies (4.4% of all films), Animation (2% of all films), and Family movies (4.3% of all films).
*	Crowd-pleasers (low margin, high volume) - Crowd-pleasers have lower budgets and lower margins, and are released more frequently. Crowd-pleaser genres include Romance (8.2% of all films) and Comedy (15% of all films).

De-emphasize less profitable genres - including Action, Crime, Thriller, and Drama.

## Keyword analysis 
Do movies with certain plot keywords have more successful outcomes? 
 
More than one plot keyword may be associated with a movie. For this analysis, a movie’s outcomes are included in the aggregate outcome for each plot keyword associated with that movie. For example - a movie whose plot keywords are "doctor" and "scientist" will be included in the analyses for both keywords. 
 
The list of movies is filtered to only show keywords (‘plot_keywords’) associated with at least 30 movies. There are 6612 keywords todtal, but only 51 are associated with at least 30 movies.

There are 4 keywords with average normalized profit greater than the profit baseline, and 19 with average normalized ROI greater than the ROI baseline.  
*	Movies with the plot keywords 'wedding', 'island', 'female nudity', and 'hospital' are the most profitable, on average.
*	Movies with the plot keywords 'high school', 'school', 'secret', 'serial killer', and 'friendship' have the highest average ROI.
*	Movies with the plot keywords 'small town', 'writer', 'escape', 'scientist', 'boy', 'rescue','future', and 'box office flop' are not profitable, on average.
*	Movies with the plot keywords 'scientist', 'box office flop' have negative ROI, on average.

There are some keywords with a negative average profit, but positive average ROI. This indicates that there is likely great variation in the outcomes for each movie associated with a given plot keyword. Additional analysis may provide insights into what features lead to success for a given keyword. For example - 25 out of the 32 movies that are tagged with the keyword "future" lost money, and therefore have a negative ROI. However, the Shane Carruth film 'Primer' gained a cult following, and has an ROI of almost 60 - which skews the average ROI value upward.

**Recommendation**
The plot keywords with the highest average roi and profit are likely to be associated with financially successful films. However, there is likely to be significant variation within each keyword, so the top-line results should be taken with a grain of salt. Additional analysis is needed to acquire a fuller understanding of which keywords are likely to produce consistent results.

## Conclusion
The analysis identified groups of lead actors, supporting actors, and directors whose movies are financially successful, on average. I also recommended that the studio focus on two genre groupings - blockbusters (high margin, low volume films), and crowd-pleasers (low margin, high-volume films – and deemphasize less profitable genres. Finally, I identified keywords that have high average profit and ROI – as well as keywords with weak results. These keywords provide direction for which plot themes the studio should embrace and avoid in the future.

Recommendations:
* Lead and Supporting Actors
  * The analysis identified lead and supporting actors with a history of strong financial outcomes. These actors should be considered for future projects.
  * I also discovered that most of the top actors by profit and ROI are inexperienced. Therefore, the studio should collect and analyze data to try and identify the determinants of success for inexperienced actors. Potential data points include: 
    * experience acting in non-movie projects (such as TV shows, theatre productions, or comedy shows)
    * financial and popular success of non-movie projects
* Directors
  * I identified directors with a history of strong financial outcomes. These directors should be considered for future projects.
  * Similar to the results for actors, I also found that many top directors by average profit and ROI are inexperienced. The studio should look for opportunities to connect with up-and-coming directors, as well as identify the determinants of success for inexperienced directors. Potential data points include: 
    * experience directing non-movie projects (such as TV shows or music videos)
    * experience working as a producer, writer, camera operator, or in another production-oriented role on a movie or non-movie projects
* Genres - focus on growth in two categories:
  *	Blockbusters
    *	high margin, low volume
    *	genres: Action, Adventure, Fantasy, Animation, and Family movies
  *	Crowd-pleasers
    * low margin, high volume	 
    *	genres: Romance and Comedy movies
* Plot keywords
  * I identified the plot keywords with the highest average gross and profit, as well as the keywords that are unprofitable, on average. Further analysis is needed to determine which keywords are associated with consistent strong results.

 ## Ideas for Additional Analysis
 
This is not an exhaustive analysis of all the elements that could contribute to the financial success of a movie. Additional analysis could be performed on the data in the dataset provided:
*	How successful are sequels and series'?
*	Closer look at popular groupings of genres (i.e. romance and comedy; action and adventure).
*	Closer look at popular groupings of keywords.
*	Group similar keywords together. (i.e. ‘marriage’, ‘marriage ceremony’, and ‘marriage proposal’ are all separate keywords – but it may be useful to analyze their results together. 
* Analysis of outcomes by content rating.

While this analysis focuses on increasing revenue for the movie studio, the studio could also explore strategies for cutting costs using more detailed budget data. Moreover, the studio could explore distribution strategies using data on revenue sources (movie theatres, streaming services, television replays, etc.).

