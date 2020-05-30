# Quibi Advertising Recommendations with Web API and Scraping

#### Overview: [1A. Gathering Reddit Data](https://github.com/scaress21/reddit_and_quibi/blob/master/code/01A_Gathering_Reddit_Data.ipynb) | [1B. Gathering Quibi Data](https://github.com/scaress21/reddit_and_quibi/blob/master/code/01B_Gathering_Quibi_Data.ipynb) | [2. Cleaning](https://github.com/scaress21/reddit_and_quibi/blob/master/code/02_Cleaning.ipynb) | [3. EDA](https://github.com/scaress21/reddit_and_quibi/blob/master/code/03_EDA.ipynb) | [4. Modeling](https://github.com/scaress21/reddit_and_quibi/blob/master/code/04_Modeling.ipynb) | [5. Comparing Reddit & Quibi](https://github.com/scaress21/reddit_and_quibi/blob/master/code/05_Comparison%20w%20Quibi%20Data.ipynb)

Quibi is a new mobile-only streaming platform that launched April 2020. All of the shows are serial and have episodes under 10 minutes. They have lots of big names doing shows such as Chrissy Tiegen and Sophie Turner. Quibi stands for "quick bites" as the content is meant to be consumed during "in between" times of your day. Since the platform is brand new, I want to analyze how well their content compares to that of other popular media (**videos, television, and podcasts**) and eventually make recommendations for advertising the individual shows in other media.

- [Videos](https://www.reddit.com/r/videos/): The length of the content is most similar to videos found on services like YouTube and Vimeo.
- [Television](https://www.reddit.com/r/television/): Given the star power and financial backing of each project, they are definitely going for the narrative and production quality of television shows.
- [Podcasts](https://www.reddit.com/r/podcasts/): As mentioned earlier, the content is meant to be consumed while you're waiting or in between tasks. Podcasts are often consumed in a similar manner. 

## Problem Statement
Given Quibi is a new platform that draws on aspects of other media, how can they most effectively reach their target audience? What shows align with the interests of video, television, and podcast consumers?

## Data Overview
To solve this problem, I drew data from four sources. Three were the subreddits mentioned above and the fourth was the show info directly from the Quibi website. From Reddit, the data pulled contained a large number of columns but many had missing values. The main columns of interest were the title of the post, the selftext (main content) of the post, plus the id and time it was created to make sure each post was unique. 

For the Quibi shows, the data pulled contained the show title, description, genre and a list of key cast/crew members. 

## Exploratory Data Analysis
To become familar with the data, I created several features that were attributes of the text but not explicitly stated such as character/word count and sentiment analysis compound score. While these had interesting results, it didn't influcence the modeling process very much since the goal was to categorize show descriptions from Quibi. These descriptions will largely be the same length. Sentiment may have helped but I wanted to focus on what words, concepts, and ideas would connect with the submission on the subreddits.

The only EDA that ended up impacting the model was visualzing what terms had high coefficients. Some of the words with large coefficients were too obvious (i.e. 'podcast' for the podcast subreddit). Theses were then turned into stop words for future itertaions of the model. If I were to do this part again, I would put all my energy into this  because it yields the most interesting inferences. By generating the stop words, I had a lot of control over what I wanted my model to see. It would be interesting to explore options for making this more objective for the goal of it being more helpful.

## Modeling
I tried a variety of models including Naive Bayes, Decision Trees and even Voting Classifier, but the one that regularly had the highest accuracy was Multinomial Logistic Regression. To preprocess the text, I used Count Vectorizer with relativly few restraints (no max feature limit, low min df, high max df). Most of the limitation came from the stop words. While this hurt the accuracy, it made the interpretation much more useful.

## Conclusions and Recommendations
After running the Quibi show descriptions through the model, it classified 19 shows for Podcasts, 22 shows for TV, and 12 shows for video. The implication here is that the shows align with the interests of podcast, TV, and video consumers and should be marketed on those platforms respectively. These were the top 3 shows for each media:

**Podcasts**
- Sports AM by TSN - Sports, News 
- Speedrun by Polygun - Gaming 
- POP5 - News, Music

**TV**
- Most Dangerous Game - Action, Thriller 
- Prodigy -  Sports, Documentary 
- Dishmantled - Cooking Competition


**Video**
- The Sauce -  Dance Competition 
- Weather Today by the Weather Channel - Weather
- Auga Donkeys - Buddy Comedy


Many of the shows had high probability for their particular class (above 95%), but it was also interesting to see where shows fell in the center (close to equal probability between classes) and might be good for advertising on multiple platforms.

This framework provided a lot of interesting conclusions about similarties between Quibi shows and subreddit audiences. If I were to continue to work on this, I would definitely focus on the stop words more. Creating a more robust way to filter will only draw stronger insights. I would also look for additional and/or segmented sources. Maybe there are other subreddits for not just videos, but YouTube, Vimeo, or content specific forums. Or perhaps it would be beneficial to consider a wider variety of sources. Overall, this project helped me learn a lot about the uses for NLP as well as multiclass classification problems. I'm proud of the results because of how applicable it is and look forward to exploring ways to improve the model.
