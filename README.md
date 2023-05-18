# DSC80 Project 3

Brandon Dioneda, Samuel Zhang

## Introduction and Question Identification

### Provide an introduction to your dataset

This dataset contains match data (win/loss, performance stats, etc.) relating to competitive League of Legends matches from the year 2022.

### Clearly state the one question your analysis is centered around

The question we would like to answer is: "Is Talon (tutor Costin’s favorite champion) more likely to win or lose any given match?"

### Why should readers of your website care about the dataset and your question specifically?

League of Legends is one of the world's most popular games and there is an intensely competitive landscape that surrounds it. Over a hundred million dollars have been awarded throughout the years as prize money, so it's no surprise that people take these competitions seriously. The slightest edges in strategy/game understanding can accumulate into a significant advantage that leads one and their team to a decisive victory.

While Talon here is a very specific example, in general, understanding the relevance of champions in the meta, is a crucial piece of game knowledge for any competitive player.

### Report the number of rows in the dataset

Matches are represented by 12 rows. 10 rows are for each of the players (5 from each team), and 2 rows are for team wide statistics.
Since there are 149400 rows total, that means there are 149400 / 12 = 12450 competitive matches contained within this dataset.
12450 _ 2 = 24900 rows are team related rows and 12450 _ 10 = 124500 rows are related to individual players.

### Names of the columns that are relevant to your question & descriptions of those relevant columns

(we're focusing on the player rows {not the team rows})
champion - the name of the champion a character has selected
result - whether that player has won the match

These two columns are needed to find matches related to Talon (champion) & wether Talon won or not (result).

## Data Cleaning

Steps Taken:

- Removing Team Statistic Related Rows

CLEANED DF:

<iframe src="./cleaned-head.html" width=800 height=600 frameBorder=0></iframe>

## Univariate Analysis

Bar graph keeps track of the total amount of times a champion is used.

## Bivariate Analysis
