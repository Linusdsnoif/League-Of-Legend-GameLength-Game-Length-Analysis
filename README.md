# League of Legends Gamelength Statistical Analysis

League of Legends Gamelength analysis is a data science project exploring the relationship between gamelength and stats. The project includes hypothesis testing, statistical analysis, baseline models, and concludes with fairness analysis. The primary goal for the project is to able to predict the possible gamelength given by the stats differnce between both teams at 25mins. 

Authors: Linus Lee

## Introduction
### Game Introduction
League of Legend is a 2009 multiplayer online battle arena video game developed and published by Riot Games. In the game, two teams of five players battle in player-versus-player combat, each team occupying and defending their half of the map. The data set the project will be working on is a professional data set that’s developed by Oracle's Elixir. The file records match data from professional LOL esports gaming matches throughout 2022. 

This dataset captures key gameplay statistics and outcomes from all profession LOL match throughout 2022, offering various features such as individual player performance, champions pick, in-game statistics, and overall match summary.

In the game of League of Legends (LOL), a power of a champion is based on five main category: xp(experience), gold, kills, assists, and cs(minionkills and monsterkills). Xp could help a champion to level up, gold helps a champion to buy items, kills and assists help champion to win advantage and gold in the game, and minionkills are the fundamental of the game to help a player to win gold and control the lanes when fighting against the opponent. If a team can have higher advantage at these five features then the team has higher chance to win the game and end the game sooner. These five features serves as an important feature of a match. 

The central question we are interested in is **Given by the stats difference between both team, are we ablt to predict the game length of the match**. The project is going to use data analysis techniques to testify the impact of five features including xp(experience), gold, kills, assists, and cs(minionkills)). At the end, the project is going to use these statistics and other important feature to set up a prediction model to predict the gamelength of a match.

### Columns Introduction
The dataset introduces a comprehensive array of columns featuring gameplay metrics and match outcomes from professional League of Legends esports matches. The data set has 150180 rows, and here is an introduction to some of the key columns the project is going to work on:

- `killsat15` : One team's count of kill for each individual player and team at 15mins.

- `assistsat15` : One team's count of assists for each individual player and team at 15mins.

- `opp_killsat15` : The opponent's count of kill for each individual player and team at 15mins.

- `opp_assistsat15` : The opponent's count of assists for each individual player and team at 15mins.
  
- `killsdiffat15` : The 'killsdiffat15' is the new column createdd that finds the total difference of kills(killsat15 - opp_killsat15) between both teams at 15mins.

- `assistsdiffat15`: The 'assistsdiffat15' is the new createdd that finds the total difference of assists(assistsat15 - opp_assistsat15) between both teams at 15mins.

- `xpdiffat15` : The 'xp' column records the total difference of experience between both team at 15mins.

- `golddiffat15` : The 'gold' column records the total difference of gold between both team at 15mins.

- `csdiffat15` : This column records the total differnce of number of minions or neutral monsters slain by a player or team during the match between both team.
  
- `league`: The 'league' column denotes the specific league tournament in which the match took place.

- `patch` : The 'patch' column record the version of the match is playing on.

- `participantid` : This column represents a unique identifier for each player and team in a game. It allows us to distinguish each team in a match.

- `gameid` : This column represents a unique identifier for each match played. It allows us to distinguish the matches in the dataset.
  
- `gamelength` : This column records the gamelength of a match in unit of seconds.
  
## Data Cleaning and Exploratory Data Analysis
### Data Cleaning
To eliminate irrelevant column we gonna use further in the project, the dataframe would only keep the relevant columns: `killsdiffat15`, `assistsdiffat15`, `xpdiffat15`, `golddiffat15`, `csdiffat15`, `league`, `patch`, `participantid`, `gameid`, `gamelength`. Moreover, since both team in the same match would have the same absolute difference on kills, assits, xp, gold, minionskill, patch, league, so we would only keep one team row for each math. In this case, we only going to keep participantid = 100. Furthermore, among these columns, since we going to predict the gamelength based on the stats difference at 15mins, so the data set is going to drop any missing value in gamelength and stats difference at 15mins.  

Below is the head of the dataframe. **The dataframe is only going to be used for the hypothesis testing**

| gameid                |   participantid |   gamelength |   golddiffat15 |   xpdiffat15 |   csdiffat15 |   killsdiffat15 |   assistsdiffat15 |
|:----------------------|----------------:|-------------:|---------------:|-------------:|-------------:|----------------:|------------------:|
| ESPORTSTMNT01_2690210 |             100 |         1713 |            107 |        -1617 |          -23 |              -1 |                -8 |
| ESPORTSTMNT01_2690219 |             100 |         2114 |          -1763 |         -906 |          -22 |              -2 |                -2 |
| ESPORTSTMNT01_2690227 |             100 |         1972 |           1191 |         2298 |           15 |               2 |                 7 |
| ESPORTSTMNT01_2690255 |             100 |         2488 |            550 |        -1259 |          -40 |               2 |                 6 |
| ESPORTSTMNT01_2690264 |             100 |         2020 |           1478 |          204 |           -9 |               0 |                 4 |


### Univariate Analysis
Below is the univariate analysis of kills difference at 15 mins.

<iframe
  src="assets/univariate_kill.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The histogram shows that the distribution of kills difference at 15mins is normal. This suggests that the data is normally distributed and well-behanved.

Below is also a univariate analysis of gamelength.

<iframe
  src="assets/univariate_game_length.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The histrogram shows that the distribution is almost nearly normal despite slightly skewness to the right, but overall the gamelength is noramlly distributed 
suggesting that the data is well distributed.

### Bivariate Analysis

The scatterplot below is bivariate analysis between the relationship of gamelength and minions kill difference at 15mins.

<iframe
  src="assets/bivariate_minion_kill.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The scatterplot we have seem to follow a trend that as the actual gamelength is longer, the difference of minions kills at 15mins between both teams seem to be smaller because the advantage for one of the team is gonna be smaller comparing to when gamelength is shorter, the difference of minion kills at 15mins is gonna be much significant.

### Interesting Aggregate

The dataframe below seem to provide some interesting aggregate for our project.

| gamelength        |   golddiffat15 |   xpdiffat15 |   csdiffat15 |   killsdiffat15 |   assistsdiffat15 |   sum_diff |
|:------------------|---------------:|-------------:|-------------:|----------------:|------------------:|-----------:|
| (937.999, 1864.0] |        336.487 |      74.4216 |     0.230162 |       0.228281  |         0.283189  |   411.651  |
| (1864.0, 3467.0]  |        159.4   |    -106.031  |    -1.84314  |      -0.0128205 |        -0.0279035 |    51.4853 |

*The **sum_diff** column is the sum of (golddiffat15, xpdiffat15, csdiffat15, killsdiffat15, assistsdiffat15)
**We will using q-cut gamelength for the upcoming hypothesis test to simplify the procedure**

In the aggregate dataframe, I have q-cut the gamelength into 2 equal proportion of segment of gamelength, and groupby the gamelength and find the mean of each features. The aggretate seem to provide interesting facts that gamelength that is shorter have larger mean sum_diff and more assistsdiff, more killsdiff, more golddiff than longer gamelength.

## Assessment of Missingness
### NMAR Analysis
In our dataset, I believe the columns `playername` are all Not Missing At Random (NMAR). Looking into the columns, we see that all these `playername` columns do not have any specific trends of missing, or any evidence of depending on other columns. In the actual League of Legends game, the players may be got fired or call up to the team the day before or at the gameday and therefore there are not many information regarding the player's information resulting the missingness of the `playername` column. One column I would obtain to make the `playername` become MAR is the  `duration_on_the_team`. For player on the team with 0 duration may be show that the player is new to the team, so there may be little or no information about the player.

### Missingness Dependency

In this part, we are going to test if the missingness of `killsat25` column depends on other columns. The two other columns that we used are `firstbloodkill` and `patch`. The significance level we choose for both permutation tests is 0.05, and the test statistic is Total Variance Distance (TVD).

First, we are going to perform the permutation test on `killsat25` and `firstblood`. 

**Null Hypothesis**: Distribution of `firstblood` when `killsat25` is missing is the same as the distribution of `firstblood` when `killsat25` is not missing.

**Alternative Hypothesis**: Distribution of `firstblood` when `killsat25` is missing is NOT same as the distribution of `firstblood` when `killsat25` is not missing.

Below is the observed distribution of `firstblood` when `killsat25` is missing and not missing.

|   firstbloodkill |     False |      True |
|-----------------:|----------:|----------:|
|                0 | 0.715886  | 0.184154  |
|                1 | 0.0795429 | 0.0204171 |

After the permutation tests, the **observed statistic** for this permutation test is: 0.29542911938628735, and the **p-value** is 0.44. The plot below shows the empirical distribution of the TVD for the test.

<iframe
  src="assets/first_blood_miss.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Since the p-value is larger than 0.05 significance level, therefore we are **fail to reject** null hypothesis, so the missingness of killsat25 **does not** depend on `firstbloodkill` column.

Furthermore, we are going to perform the permutation test on `killsat25` and `patch`. 

**Null Hypothesis**: Distribution of `patch` when `killsat25` is missing is the same as the distribution of `patch` when `killsat25` is not missing.

**Alternative Hypothesis**: Distribution of `patch` when `killsat25` is missing is NOT same as the distribution of `patch` when `killsat25` is not missing.

Below is the observed distribution of `patch` when `killsat25` is missing and not missing.

|   patch |       False |          True |
|--------:|------------:|--------------:|
|   12.01 | 0.0529346   |   0.0111946   |
|   12.02 | 0.0561331   |   0.0212698   |
|   12.03 | 0.0654086   |   0.00471774  |
|   12.04 | 0.066768    |   0.0392612   |
|   12.05 | 0.0844395   |   0.0153526   |
|   12.06 | 0.0135935   |   0.00135935  |
|   12.07 | 0.00615704  |   0.000399808 |
|   12.08 | 0.0120742   |   0.00239885  |
|   12.09 | 0.0260675   |   0.002079    |
|   12.1  | 0.0466176   |   0.00735647  |
|   12.11 | 0.0588518   |   0.0168719   |
|   12.12 | 0.0893971   |   0.0191908   |
|   12.13 | 0.0568527   |   0.0226291   |
|   12.14 | 0.037502    |   0.0099952   |
|   12.15 | 0.0299056   |   0.0068767   |
|   12.16 | 0.0212698   |   0.00751639  |
|   12.17 | 0.00191908  | nan           |
|   12.18 | 0.0377419   |   0.00511754  |
|   12.19 | 0.0134336   |   0.00255877  |
|   12.2  | 0.0109547   |   0.000959539 |
|   12.21 | 0.00719655  |   0.000799616 |
|   12.23 | 0.000719655 |   0.00615704  |

After the permutation tests, the **observed statistic** for this permutation test is: 0.30041580041580035, and the **p-value** is 0. The plot below shows the empirical distribution of the TVD for the test.

<iframe
  src="assets/patch_miss.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



