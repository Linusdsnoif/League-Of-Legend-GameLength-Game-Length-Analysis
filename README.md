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

Our p-value is smaller than 0.05 significance level, therefore we **reject** null hypothesis, and therefore the missingness of killsat25 **does** depend on `patch` column.

## Hypothesis Testing
For the hypothesis test, the project aim to assess whether there is a relationship between the gamelength and the mean of sum differnce of stats(`golddiffat15`, `xpdiffat15`, `csdiffat15`,`killsdiffat15`,`assistsdiffat15`, `sumdiffat15`) at 15mins. The investigation of relationship is better because it helps us understanding the impact of building early advantage in the game to the gamelength.

Here is the head of dataframe we going to perform our hypothesis testing.

|     | gamelength        |   sum_diff |
|----:|:------------------|-----------:|
|  10 | (937.999, 1864.0] |      -1542 |
|  46 | (1864.0, 3467.0]  |       3513 |
|  94 | (1864.0, 3467.0]  |       1677 |
| 142 | (1864.0, 3467.0]  |      -3359 |
| 166 | (1864.0, 3467.0]  |      -1799 |

This is the example of dataframe to perform our tvd test statistic

| gamelength        |   sum_diff |
|:------------------|-----------:|
| (937.999, 1864.0] |   411.651  |
| (1864.0, 3467.0]  |    51.4853 |

**Null**: The distribution of mean of sum stats difference at 15mins for first quantile of gamelength is the same as the distribution of stats difference at 15mins for second quantile of gamelength

**Alternative**: The distribution of mean of sum stats difference at 15mins for first quantile of gamelength is Not the same as the distribution of stats difference at 15mins for second quantile of gamelength

**Test Statistics**: TVD

**Significance Level**: 0.05

After performing the permutation test on `sum_diff` column for 1000 times, our **observed test statistic** is: 360.16532641638827, and our **p-value** is: 0.008.

Here is a histogram containing the distribution of our test statistics during the hypothesis test:

<iframe
  src="assets/hypothesis.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Our p-value is smaller than 0.05 significance level, therefore we **reject** null hypothesis, and this suggests the distribution of mean of sum stats difference at 15mins for first quantile of gamelength is Not the same as the distribution of stats difference at 15mins for second quantile of gamelength. The finding lead to the concept that the level of difference of stats at 15mins may affect the gamelength.

## Framing a Prediction Problem
From the hypothesis testing, we found out that getting huge difference of stats at 15mins may contribute to the length of the game, and therefore I hope to extend the finding to further extent. Since the game at 15mins still has a lot of factors that may deeply affect the outcome of the game. Is it possible to predict the gamelength by giving the stats difference at 25mins and the information about the feature of patch and the league?

To address this finding, we can employ Linear Regression model to predict the possible gamelength given by the stats. For our prediction model, we will focus on the stats difference at 25mins and the version of patch and the name of the league in order to enhance our precision.

In this part, we will one-hot encode the original `league` and `patch` column, and we will create a new `sum_diff`(would only contains the sum of xpdiffat25, golddiffat25, and csdiffat25), and we will square root the column of `killsassist`(sum of `killsdiffat25` and `assistsdiffat25`). As we are only predicting the gamelength based on the these features, we are going to drop the remaining irrelevant columns. 

Below is the head of DataFrame we are using in this section: 

|    | league   |   patch |   sum_diff |   killsassists |
|---:|:---------|--------:|-----------:|---------------:|
| 10 | LCKC     |   12.01 |       3980 |             11 |
| 22 | LCKC     |   12.01 |      15059 |             19 |
| 46 | LCKC     |   12.01 |       6682 |             14 |
| 70 | LCKC     |   12.01 |       4920 |             12 |
| 94 | LCKC     |   12.01 |       3838 |             12 |

Our data will split into 80% training data and 20% testing data, and since our model is a regression our model, so we going to choose RMSE and R^2 as our metrics to evaluate our model performance as it could provide the most straightforward performance on how good is our prediction.

## Baseline Model
For the baseline model, we used a Linear Regression model, with the following two features: `sum_diff` and `patch`. The `sum_diff` is a quantitative column, so therefore we can leave the column as-is. However, the `patch` column is a categorical column, so therefore we will perform the OneHotencoding in our pipeline and at the end using the Lienar Regression model to predict the gamelength.

After fitting the model, our R^2 score for the training data is: **0.3685153110578967**, and the RMSE for training data is: **63446.681449617434**. On the other hand, for the testing data the R^2 score is **0.36400612680386324**, and the RMSE for testing data is: **62835.21088187913**. The performance is considered acceptable since the game could be affected by various aspects such as strategy, player behavior, and even luck. There are various outside factors outside and inside the game.

## Final Model
In our final model, we added two more features: `league` and `killsassists`. We are adding these two features into our model because we believe that different league has different culture and would affect the gamelength differently such as player in Europe may play much aggressive than player in North America and therefore may shorten the gamelength than other areas. The `killsassists` column would enhave our precision because in League of Legend having a kill or assists could bring gold and xp to a player and therefore would help the model to evaluate the advantage of a player and a team.

Our final model is going to use Lasso regression model. The two additional features we added (`league` and `killsassists`) the `league` is categorical column, so we going to employ OneHotencoder to the column and we also going to employ square root transformer to our `killsassists` column. In terms of tuning hyperparameters, the hyperparameter I chose is: **alpha** for the Lasso regression model. I am using the GridSearchCV to find the best possible alpha for Lasso in our regression model. At the end, we find that the best alpha possible by using GridSearchCV is: **0.5963623316594643**.

After fitting the model, our R^2 score for the training data is now improve to: **0.38012948662203216**, and the RMSE for training data is now improve to: **62279.77921078074**. On the other hand, for the testing data the R^2 score is **0.3851375657358337**, and the RMSE for testing data is now: **60747.45740265901**. The improvement performance is quite substaintial. It is suggested that the model has now improved its ability to predict the gamelength.

## Fairness Analysis
In this section, we are going to assess if our model is fair among different areas. The question we are trying to answer here is: **“does my model perform worse for games that happen in LCKC or games that are not happen in LCKC"** To answer this question, we performed a permutation test and examined the result of the difference in RMSE between the two groups. 

The followings are the hypothesis:

**Null hypothesis**: Our model is fair. Its RMSE of gamelength for games that happened in LCKC league is the same as the RMSE of gamelength for games that happened in league other than LCKC.

**Alternative hypothesis**: Our model is unfair.Its RMSE of gamelength for games that happened in LCKC league is NOT the same as the RMSE of gamelength for games that happened in league other than LCKC.

**Test statistics**: TVD

**Significance Level**: 0.05

Below is the histogram of our test statistics:

<iframe
  src="assets/fairness.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

After performing the permutation test, the result p-value we got is **0.595**, which is larger than the 0.05 significance level. Consequently, we **fail to reject** the null hypothesis. This outcome implies that our model predicts gamelength from games in LCKC and other than LCKC is similar. Consequently, our model appears to be fair that does not show obvious discrimination between both group.
