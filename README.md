# DSC80 Project 3

Brandon Dioneda, Samuel Zhang

## Introduction and Question Identification

** Provide an introduction to your dataset **

This dataset contains match data (win/loss, performance stats, etc.) relating to competitive League of Legends matches from the year 2022.

** Clearly state the one question your analysis is centered around **

The question we would like to answer is: "Is Talon (tutor Costin’s favorite champion) more likely to win or lose any given match?"

** Why should readers of your website care about the dataset and your question specifically? **

League of Legends is one of the world's most popular games and there is an intensely competitive landscape that surrounds it. Over a hundred million dollars have been awarded throughout the years as prize money, so it's no surprise that people take these competitions seriously. The slightest edges in strategy/game understanding can accumulate into a significant advantage that leads one and their team to a decisive victory.

While Talon here is a very specific example, in general, understanding the relevance of champions in the meta, is a crucial piece of game knowledge for any competitive player.

** Report the number of rows in the dataset **

Matches are represented by 12 rows. 10 rows are for each of the players (5 from each team), and 2 rows are for team wide statistics.
Since there are 149400 rows total, that means there are 149400 / 12 = 12450 competitive matches contained within this dataset.
12450 _ 2 = 24900 rows are team related rows and 12450 _ 10 = 124500 rows are related to individual players.

** Names of the columns that are relevant to your question & descriptions of those relevant columns **

(we're focusing on the player rows {not the team rows})
champion - the name of the champion a character has selected
result - whether that player has won the match

These two columns are needed to find matches related to Talon (champion) & wether Talon won or not (result).

## Data Cleaning

Describe, in detail, the data cleaning steps you took and how they affected your analyses. The steps should be explained in reference to the data generating process. Show the head of your cleaned DataFrame (see Part 2: Report for instructions).

Steps Taken to Clean the Data

<!-- - Removing Rows marked with data incompleteness:

  - There are rows marked as complete, partial, or ignore. Competitive League matches that were left incomplete for whatever reason (abandoning, reset, etc.) are not going to accurately represent the performance of Talon.
  - Over 10 rows related to Talon matches are removed through filtering out these columns. As a result, the number of talon rows that are left to perform our analysis on only number to 50. -->

- Drop Team Related Columns

  - There are both player and team statistic rows inside the dataset. Since we're only interested in the performance of a particular champion, it doesn't make sense to have rows that don't have any champion information.
  - We could technically keep these rows without having any effect on our analysis (NaN values will be ignored). However, removing these rows keeps our dataframe more interpretable. (Won't confuse readers who may not be familiar with the structure of the dataset)

- Drop Team Related Columns

  - Along with team-related rows, there are also team-related columns, where for all player-related rows the value for that column would be NaN.
  - Since all the team-related rows have been dropped, these columns bring nothing of value to our analysis. They will only serve to visually clutter the dataframe.

- Replace "unknown player" with NaN in playername column

  - Unknown players are currently denoted with the string "unknown player".
  - Since the playername column is a string column, potential analyses can misinterpret "unknown player" as being an actual player.

- Casting Columns to bool

  - There are a lot of columns that are essentially True/False values. However, these values are denoted by 0 or 1. As a result, the datatype can be misinterpreted as an integer instead of a boolean value.
  - Checking to see if columns are T/F
    - Create a set of values within the column. If they're 0/1, then convert values in column to T/F

- Convert Data Types
  - Running the pandas convert_dtypes function on the dataset. Infers string, integer, and float types when appropiate.

HEAD OF CLEANED DF (5 rows x 97 columns):

<div markdown="1" style="
    display: block; 
    /* background-color: blue;  */
    width: 100%; 
    overflow-x:auto
">

|     | gameid                | datacompleteness | url  | league | year | split  | playoffs | date                | game | patch | participantid | side | position | playername | playerid                                  | teamname                 | teamid                                  | champion | ban1  | ban2    | ban3   | ban4   | ban5 | gamelength | result | kills | deaths | assists | teamkills | teamdeaths | doublekills | triplekills | quadrakills | pentakills | firstblood | firstbloodkill | firstbloodassist | firstbloodvictim | team kpm |   ckpm | barons | opp_barons | inhibitors | opp_inhibitors | damagetochampions |     dpm | damageshare | damagetakenperminute | damagemitigatedperminute | wardsplaced |    wpm | wardskilled |   wcpm | controlwardsbought | visionscore |   vspm | totalgold | earnedgold | earned gpm | earnedgoldshare | goldspent | total cs | minionkills | monsterkills |   cspm | goldat10 | xpat10 | csat10 | opp_goldat10 | opp_xpat10 | opp_csat10 | golddiffat10 | xpdiffat10 | csdiffat10 | killsat10 | assistsat10 | deathsat10 | opp_killsat10 | opp_assistsat10 | opp_deathsat10 | goldat15 | xpat15 | csat15 | opp_goldat15 | opp_xpat15 | opp_csat15 | golddiffat15 | xpdiffat15 | csdiffat15 | killsat15 | assistsat15 | deathsat15 | opp_killsat15 | opp_assistsat15 | opp_deathsat15 |
| --: | :-------------------- | :--------------- | :--- | :----- | ---: | :----- | :------- | :------------------ | ---: | ----: | ------------: | :--- | :------- | :--------- | :---------------------------------------- | :----------------------- | :-------------------------------------- | :------- | :---- | :------ | :----- | :----- | :--- | ---------: | :----- | ----: | -----: | ------: | --------: | ---------: | ----------: | ----------: | ----------: | ---------: | :--------- | :------------- | :--------------- | :--------------- | -------: | -----: | -----: | ---------: | ---------: | -------------: | ----------------: | ------: | ----------: | -------------------: | -----------------------: | ----------: | -----: | ----------: | -----: | -----------------: | ----------: | -----: | --------: | ---------: | ---------: | --------------: | --------: | -------: | ----------: | -----------: | -----: | -------: | -----: | -----: | -----------: | ---------: | ---------: | -----------: | ---------: | ---------: | --------: | ----------: | ---------: | ------------: | --------------: | -------------: | -------: | -----: | -----: | -----------: | ---------: | ---------: | -----------: | ---------: | ---------: | --------: | ----------: | ---------: | ------------: | --------------: | -------------: |
|   0 | ESPORTSTMNT01_2690210 | complete         | <NA> | LCK CL | 2022 | Spring | False    | 2022-01-10 07:44:08 |    1 | 12.01 |             1 | Blue | top      | Soboro     | oe:player:38e0af7278d6769d0c81d7c4b47ac1e | Fredit BRION Challengers | oe:team:68911b3329146587617ab2973106e23 | Renekton | Karma | Caitlyn | Syndra | Thresh | Lulu |       1713 | False  |     2 |      3 |       2 |         9 |         19 |           0 |           0 |           0 |          0 | False      | False          | False            | False            |   0.3152 | 0.9807 |      0 |          0 |          0 |              0 |             15768 | 552.294 |    0.278784 |               1072.4 |                  777.793 |           8 | 0.2802 |           6 | 0.2102 |                  5 |          26 | 0.9107 |     10934 |       7164 |    250.928 |        0.253859 |     10275 |      231 |         220 |           11 | 8.0911 |     3228 |   4909 |     89 |         3176 |       4953 |         81 |           52 |        -44 |          8 |         0 |           0 |          0 |             0 |               0 |              0 |     5025 |   7560 |    135 |         4634 |       7215 |        121 |          391 |        345 |         14 |         0 |           1 |          0 |             0 |               1 |              0 |
|   1 | ESPORTSTMNT01_2690210 | complete         | <NA> | LCK CL | 2022 | Spring | False    | 2022-01-10 07:44:08 |    1 | 12.01 |             2 | Blue | jng      | Raptor     | oe:player:637ed20b1e41be1c51bd1a4cb211357 | Fredit BRION Challengers | oe:team:68911b3329146587617ab2973106e23 | Xin Zhao | Karma | Caitlyn | Syndra | Thresh | Lulu |       1713 | False  |     2 |      5 |       6 |         9 |         19 |           0 |           0 |           0 |          0 | True       | False          | True             | False            |   0.3152 | 0.9807 |      0 |          0 |          0 |              1 |             11765 | 412.084 |    0.208009 |              944.273 |                  650.158 |           6 | 0.2102 |          18 | 0.6305 |                  6 |          48 | 1.6813 |      9138 |       5368 |    188.021 |         0.19022 |      8750 |      148 |          33 |          115 | 5.1839 |     3429 |   3484 |     58 |         2944 |       3052 |         63 |          485 |        432 |         -5 |         1 |           2 |          0 |             0 |               0 |              1 |     5366 |   5320 |     89 |         4825 |       5595 |        100 |          541 |       -275 |        -11 |         2 |           3 |          2 |             0 |               5 |              1 |
|   2 | ESPORTSTMNT01_2690210 | complete         | <NA> | LCK CL | 2022 | Spring | False    | 2022-01-10 07:44:08 |    1 | 12.01 |             3 | Blue | mid      | Feisty     | oe:player:d1ae0e2f9f3ac1e0e0cdcb86504ca77 | Fredit BRION Challengers | oe:team:68911b3329146587617ab2973106e23 | LeBlanc  | Karma | Caitlyn | Syndra | Thresh | Lulu |       1713 | False  |     2 |      2 |       3 |         9 |         19 |           0 |           0 |           0 |          0 | False      | False          | False            | False            |   0.3152 | 0.9807 |      0 |          0 |          0 |              0 |             14258 | 499.405 |    0.252086 |              581.646 |                  227.776 |          19 | 0.6655 |           7 | 0.2452 |                  7 |          29 | 1.0158 |      9715 |       5945 |    208.231 |        0.210665 |      8725 |      193 |         177 |           16 | 6.7601 |     3283 |   4556 |     81 |         3121 |       4485 |         81 |          162 |         71 |          0 |         0 |           1 |          0 |             0 |               0 |              1 |     5118 |   6942 |    120 |         5593 |       6789 |        119 |         -475 |        153 |          1 |         0 |           3 |          0 |             3 |               3 |              2 |
|   3 | ESPORTSTMNT01_2690210 | complete         | <NA> | LCK CL | 2022 | Spring | False    | 2022-01-10 07:44:08 |    1 | 12.01 |             4 | Blue | bot      | Gamin      | oe:player:998b3e49b01ecc41eacc392477a98cf | Fredit BRION Challengers | oe:team:68911b3329146587617ab2973106e23 | Samira   | Karma | Caitlyn | Syndra | Thresh | Lulu |       1713 | False  |     2 |      4 |       2 |         9 |         19 |           0 |           0 |           0 |          0 | True       | False          | True             | False            |   0.3152 | 0.9807 |      0 |          0 |          0 |              0 |             11106 | 389.002 |    0.196358 |              463.853 |                  218.879 |          12 | 0.4203 |           6 | 0.2102 |                  4 |          25 | 0.8757 |     10605 |       6835 |    239.405 |        0.242201 |     10425 |      226 |         208 |           18 | 7.9159 |     3600 |   3103 |     78 |         3304 |       2838 |         90 |          296 |        265 |        -12 |         1 |           1 |          0 |             0 |               0 |              0 |     5461 |   4591 |    115 |         6254 |       5934 |        149 |         -793 |      -1343 |        -34 |         2 |           1 |          2 |             3 |               3 |              0 |
|   4 | ESPORTSTMNT01_2690210 | complete         | <NA> | LCK CL | 2022 | Spring | False    | 2022-01-10 07:44:08 |    1 | 12.01 |             5 | Blue | sup      | Loopy      | oe:player:e9741b3a238723ea6380ef2113fae63 | Fredit BRION Challengers | oe:team:68911b3329146587617ab2973106e23 | Leona    | Karma | Caitlyn | Syndra | Thresh | Lulu |       1713 | False  |     1 |      5 |       6 |         9 |         19 |           0 |           0 |           0 |          0 | True       | True           | False            | False            |   0.3152 | 0.9807 |      0 |          0 |          0 |              0 |              3663 | 128.301 |   0.0647631 |              475.026 |                  490.123 |          29 | 1.0158 |          14 | 0.4904 |                 11 |          69 | 2.4168 |      6678 |       2908 |    101.856 |        0.103054 |      6395 |       42 |          42 |            0 | 1.4711 |     2678 |   2161 |     16 |         2150 |       2748 |         15 |          528 |       -587 |          1 |         1 |           1 |          0 |             0 |               0 |              1 |     3836 |   3588 |     28 |         3393 |       4085 |         21 |          443 |       -497 |          7 |         1 |           2 |          2 |             0 |               6 |              2 |

</div>

## Univariate Analysis

<iframe src="assets/champion_freq.html" width="100%" height="500px" frameBorder=0></iframe>

(1st graph)
Bar graph keeps track of the total amount of times a champion is used. We ordered the bars from least frequent to most frequent. For the champion in question, we see that Talon is only used 50 times throughout the 2022 season.

<iframe src="assets/kills_histogram.html" width="100%" height="500px" frameBorder=0></iframe>

(2nd graph)
A density histogram of the frequency of kills a champion has overall in the data set. We included an overlayed density histogram for Talon specifically. Through the whole season, Talon mostly gets only 2-3 kills in a given match, which isn't too surprising as Talon usually takes the Jungle position.

## Bivariate Analysis

<iframe src="assets/wins_and_losses.html" width="100%" height="500px" frameBorder=0></iframe>

(1st graph)
Bar graph that keeps track of the wins and loses that each champion has, where blue depicts the wins and red the losses. Talon in particular has 28 wins and 22 losses.

<iframe src="assets/kills_vs_deaths.html" width="100%" height="500px" frameBorder=0></iframe>

(2nd graph)
We wanted to explore the relationship between the number of kills and deaths in the data set. In the scatter plot above, we see that the more kills a player has, the less deaths they have, though this association is weak as the graph isn't quite linear.

## Interesting Aggregates

<div markdown="1" style="
    display: block; 
    /* background-color: blue;  */
    width: 100%; 
    overflow-x:auto
">

| result | ('earned gpm', 'bot') | ('earned gpm', 'jng') | ('earned gpm', 'mid') | ('earned gpm', 'sup') | ('earned gpm', 'top') |
| :----- | --------------------: | --------------------: | --------------------: | --------------------: | --------------------: |
| False  |               257.326 |               178.836 |               231.934 |               87.3538 |               223.427 |
| True   |               342.339 |               245.858 |               302.895 |               133.629 |               292.377 |

</div>

(1st pivot)
Pivot table that keeps track of the average earned gpm (gold per minute) each position has, depending on if they won a match or not. As expected, the highest avergage gpm is across all positions where a match was won. In relation to our question, Talon usually takes the Jungle position whose responsibility is gaining gold and experience for the team.

<div markdown="1" style="
    display: block; 
    /* background-color: blue;  */
    width: 100%; 
    overflow-x:auto
">

| side | ('kills', 'bot') | ('kills', 'jng') | ('kills', 'mid') | ('kills', 'sup') | ('kills', 'top') |
| :--- | ---------------: | ---------------: | ---------------: | ---------------: | ---------------: |
| Blue |          4.34667 |          3.13831 |          3.55566 |         0.894378 |          2.83309 |
| Red  |          4.17092 |          2.97558 |          3.44723 |          0.85245 |          2.75639 |

</div>

(2nd pivot)
Pivot table of average kills per position depending on if they are on the Blue or Red side of a match. Trend observed is that the Blue side gets higher kills on average across all positions.

## NMAR Analysis

State whether you believe there is a column in your dataset that is NMAR. Explain your reasoning and any additional data you might want to obtain that could explain the missingness (thereby making it MAR). Make sure to explicitly use the term “NMAR.”

We believe the 'url' column may be NMAR. There are urls that exist for every competitive match, which will documenent match information. However, after checking the unique domain names in the url column, it would appear that the only the 2 sites mentioned are: lpl.qq.com & matchhistory.na.leagueoflegends.com.

The missingness of the url value depends on whether there is a url for the match that is documented on one of these two sites. In other words, the missingness of the url depends on part of the url itself, i.e. the value of the url.

## Missingness Dependency

<iframe src="assets/ban2_by_missingness_of_ban1.html" width="100%" height="500px" frameBorder=0></iframe>

Ban1 & Ban2 are both categorical variables that take on the value of the name of a champion. As a result, to determine if the value of ban2 is related to the missingness of ban1, we need to have a test statistic that tells us how different two categorical distributions are. The TVD is an appropiate choice to use here.

Our Hypotheses:
Null hypothesis - The distributions of ban2 when ban1 is missing and ban2 when ban1 isn't missing are the same.
Alternative hypothesis - The distributions of ban2 when ban1 is missing and ban2 when ban1 isn't missing are not the same.

The observed test statistic (TVD) that we calculate ends up being ~0.3599. To check to see how unusual this observed test stat is (assuming the null), we run a permutation test and simulate test statistics under the null hypothesis 100 times.

In the end, our calculated p-value ends up being exactly 0. This means that none of our simulated test statistics were ever greater than or equal to our observed test statistic.

We have sufficient evidence to reject the null hypothesis. This ultimately suggests that the categorical distribution of ban2 when ban1 is missing, is different from the categorical distribution of ban2 when ban1 isn't missing.

In other words, the missingness of ban1 is dependent on ban2. (MAR)

<iframe src="assets/result_by_missingness_of_ban1.html" width="100%" height="500px" frameBorder=0></iframe>

This time we're checking to see if the distributions of result (Boolean True/False), are different depending on if ban1 is missing or not. In this case, result is also a categorical variable, so the TVD would remain an appropiate statistic in this case as well.

Our Hypotheses:
Null hypothesis - This distributions of result when ban1 is missing and result when ban1 isn't missing are the same.
Alternative hypothesis - This distributions of result when ban1 is missing and result when ban1 isn't missing are not the same.

Our observed test statistic is ~0.00139. Once again, to figure out how unusual this test statistic is (assuming the null), we run a permutation test and simulate test statistics under the null hypothesis 100 times.

In the end, our calculated p-value is 0.9. This means that 90% of simulated test statistics ended up being greater than our observed test statistic. This means that our observed test statistic is not unusual under the null.

With this in mind, we fail to reject the null hyothesis. While result could still be dependent on the missingness on ban1, we don't have enough evidence to think that could be the case.

Subsequently, the missingness of ban1 does not depend on result.

## Hypothesis Test

Going back to our question, about whether Talon is more likely to win or lose any given match. We would essentially like to know if Talon's winrate is more than 50%.

Null Hypothesis: Talon's win rate is 50%
Alternative Hypothesis: Talon's win rate is greater than 50%

In this case, the test statistic

Test Shatistic: Talon's proportion of matches won. This is an appropiate choice of test statistic, as larger values point towards the alternative hypothesis, and smaller values point towards the null hypothesis.

Chosen Significance Level: 0.05. This means that we're willing to reject if at most 5% of our generated test statistics are more extreme than the observed test statistic. In other words, we'd be willing to accept a 5% chance of making a Type I error.

<iframe src="assets/talon_win_rate.html" width="100%" height="500px" frameBorder=0></iframe>

P-Value: 0.2323

We fail to reject the null hypothesis @ the 0.05 significance level. It should be noted that Talon's true winrate could very well be greater than 50%, and that we are making a Type II error. However, we lack sufficient evidence to definitively support this claim. To increase our power to detect an effect, we can consider increasing our sample size by including matches from other years. However, it should be noted that Talon as a hero has likely been changed (buffs/nerfs) numerous times, so we should take interpretations about how good Talon is currently, with a grain of salt. 
