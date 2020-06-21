# Investigate-a-Dataset


# Project: Investigate a Dataset (TMDB Movies Data Analysis)

## Table of Contents
<ul>
<li><a href="#intro">Introduction</a></li>
<li><a href="#wrangling">Data Wrangling</a></li>
<li><a href="#eda">Exploratory Data Analysis</a></li>
<li><a href="#conclusions">Conclusions</a></li>
</ul>


<a id='intro'></a>
## Introduction


In this project I will be analyzing the data related to TMDB movies, TMDB Movie Data contains more than 10000 movies
and specifically I will look for Top 5  movies and the relationship between revenue and other factors.
As the questions below will be addressed:

### What are the top 5 movies based on ratings?

### What kind of relationship is associated between revenue and other factors? 

# Use this cell to set up import statements for all of the packages that you
#   plan to use.
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

% matplotlib inline


<a id='wrangling'></a>
## Data Wrangling
 Firstly, I will load in the data, check for cleanliness, and then trim and clean the dataset for analysis.

### General Properties

# Load your data and print out a few lines. Perform operations to inspect data
#   types and look for instances of missing or possibly errant data.
df_tmdbmov = pd.read_csv('tmdb-movies.csv')
df_tmdbmov.head()


#the data contains 21 columns and 10866 rows
df_tmdbmov.shape


# this step will help me to understand the data 
df_tmdbmov.describe()


# this step is to figure out missing data and after that we can clean and remove unused data
df_tmdbmov.info()




## Data Cleaning (clean and remove unused data) 
 In this step I will clean and polish the data 
 
 
 # After discussing the structure of the data and any problems that need to be
#   cleaned, perform those cleaning steps in the second part of this section.
# first step is I will drop out the data that I will not use
df_tmdbmov.drop(['id','imdb_id','cast','homepage','director','tagline','keywords','production_companies','overview'], axis=1 , inplace = True)

# to check after the drop out
df_tmdbmov.head()

# these histograms can illustrate the picture more 
df_tmdbmov.hist(figsize=(10,8));

# below is the data after droping out the unused data
df_tmdbmov.info()

# geners is the only column that has a missing data, I will drop out the 23 rows to adjust the data
df_tmdbmov.dropna(inplace=True)
df_tmdbmov.info()

# checking for duplicated data
df_tmdbmov.duplicated().sum()

# drop duplicated data
df_tmdbmov = df_tmdbmov.drop_duplicates(keep=False)
df_tmdbmov.duplicated().sum()



<a id='eda'></a>
## Exploratory Data Analysis



## Research Question 1 
### What are the top 5 movies based on ratings ?


# Use this, and more code cells, to explore your data. Don't forget to add
#   Markdown cells to document your observations and findings.
df_tmdbmov = pd.read_csv('tmdb-movies.csv')
df_tmdbmov = df_tmdbmov.nlargest(5,'vote_average')
df_tmdbmov[['vote_average' , 'original_title']].head()



## Research Question 2  
### What kind of relationship is associated between revenue and other factors? 

# plot relationship between popularity and revenue
df_tmdbmov = pd.read_csv('tmdb-movies.csv')
df_tmdbmov.head()

df_tmdbmov.plot(x='popularity', y='revenue', kind='scatter');
plt.title(' Relationship Between Popularity and Revenue ' , fontsize = 11);
#The plot shows a postivie linear between popularity and revenue which means revenue increase when the movie is popular

# checking the correlation value to ensure the relationship between popularity and revenue 
revenue = df_tmdbmov['revenue']
df_tmdbmov['popularity' ].corr(revenue)

# plot relationship between budget and revenue
df_tmdbmov.plot(x='budget', y='revenue', kind='scatter');

plt.title(' Relationship Between Budget and Revenue ', fontsize = 11);
# The plot shows a postivie linear between bduget and revenue which means revenue increase when the movie has a high budget

# checking the correlation value to ensure the relationship between budget and revenue
revenue = df_tmdbmov['revenue']
df_tmdbmov['budget' ].corr(revenue)


<a id='conclusions'></a>
## Conclusions

### Report:
After analyzing the data related to TMDB movies, TMDB Movie Data contains more than 10000 movies ,the average of the movies have a run time of 102.The Top 5 movies was extracted , and it was found that 'The Story of Film: An Odyssey' movie is the top rating movie based on avergae vote,it has a rating of 9.2 which consider a high rate.Additionally, 'Pink Floyd: Pulse' took the fifth place of top rating movies.
In the other hand,the scatter plot shows a postivie linear between popularity and revenue which means revenue increase when the movie is popular.Besides, the scatter plot of budget and revenue illustrate a positive linear relationship.The value of correlation ensure the postivie relationship between revenue and the two factors.
### Limitations :
There where a missing data that was needed to be fill in which leads me to drop some rows ,and the 'genres' and 'cast' columns contain multiple values that needs to be separated.


from subprocess import call
call(['python', '-m', 'nbconvert', 'Investigate_a_Dataset.ipynb'])
