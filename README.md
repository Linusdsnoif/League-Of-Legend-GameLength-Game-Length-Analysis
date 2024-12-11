# League of Legends Gamelength Statistical Analysis

League of Legends Gamelength analysis is a data science project exploring the relationship between gamelength and stats. The project includes hypothesis testing, statistical analysis, baseline models, and concludes with fairness analysis. The primary goal for the project is to able to predict the possible gamelength given by the stats differnce between both teams at 25mins. 

Authors: Linus Lee

## General Introduction
League of Legend is a 2009 multiplayer online battle arena video game developed and published by Riot Games. In the game, two teams of five players battle in player-versus-player combat, each team occupying and defending their half of the map. The data set the project will be working on is a professional data set that’s developed by Oracle's Elixir. The file records match data from professional LOL esports gaming matches throughout 2022. 

This dataset captures key gameplay statistics and outcomes from all profession LOL match throughout 2022, offering various features such as individual player performance, champions pick, in-game statistics, and overall match summary.

In the game of League of Legends (LOL), a power of a champion is based on five main category: xp(experience), gold, kills, assists, and cs(minionkills and monsterkills). Xp could help a champion to level up, gold helps a champion to buy items, kills and assists help champion to win advantage and gold in the game, and minionkills are the fundamental of the game to help a player to win gold and control the lanes when fighting against the opponent. If a team can have higher advantage at these five features then the team has higher chance to win the game and end the game sooner. These five features serves as an important feature of a match. 

The central question we are interested in is **Given by the stats difference between both team, are we ablt to predict the game length of the match**. The project is going to use data analysis techniques to testify the impact of five features including xp(experience), gold, kills, assists, and cs(minionkills)). At the end, the project is going to use these statistics and other important feature to set up a prediction model to predict the gamelength of a match.

## Introduction of Columns
The dataset introduces a comprehensive array of columns featuring gameplay metrics and match outcomes from professional League of Legends esports matches. The data set has 150180 rows, and here is an introduction to some of the key columns the project is going to work on:

- 'killsat15' : One team's count of kill for each individual player and team at 15mins.

- 'assistsat15' : One team's count of assists for each individual player and team at 15mins.

- 'opp_killsat15' : The opponent's count of kill for each individual player and team at 15mins.

- 'opp_assistsat15' : The opponent's count of assists for each individual player and team at 15mins.
  
- 'killsdiffat15' : The 'killsdiffat15' is the new column createdd that finds the total difference of kills(killsat15 - opp_killsat15) between both teams at 15mins.

- 'assistsdiffat15': The 'assistsdiffat15' is the new createdd that finds the total difference of assists(assistsat15 - opp_assistsat15) between both teams at 15mins.

- 'xpdiffat15': The 'xp' column records the total difference of experience between both team at 15mins.

- 'golddiffat15': The 'gold' column records the total difference of gold between both team at 15mins.

- 'csdiffat15': This column records the total differnce of number of minions or neutral monsters slain by a player or team during the match between both team.
  
- 'league': The 'league' column denotes the specific league tournament in which the match took place.

- 'patch' : The 'patch' column record the version of the match is playing on.

- 'participantid': This column represents a unique identifier for each player and team in a game. It allows us to distinguish each team in a match.

- 'gameid': This column represents a unique identifier for each match played. It allows us to distinguish the matches in the dataset.
  
## Data Cleaning
To eliminate irrelevant column we gonna use further in the project, the dataframe would only keep the relevant columns: 'killsdiffat15', 'assistsdiffat15', 'xpdiffat15', 'golddiffat15', 'csdiffat15', 'league', 'patch', 'participantid', 'gameid'. Moreover, since both team in the same match would have the same absolute difference on kills, assits, xp, gold, minionskill, patch, league, so we would only keep one team row for each math. In this case, we only going to keep participantid = 100. Furthermore, among these columns, since we going to predict the gamelength based on the stats difference at 15mins, so the data set is going to drop any missing value in gamelength and stats difference at 15mins.  

Below is the head of the dataframe. **The dataframe is only going to be used for the hypothesis testing**

| gameid                |   participantid |   gamelength |   golddiffat15 |   xpdiffat15 |   csdiffat15 |   killsdiffat15 |   assistsdiffat15 |
|:----------------------|----------------:|-------------:|---------------:|-------------:|-------------:|----------------:|------------------:|
| ESPORTSTMNT01_2690210 |             100 |         1713 |            107 |        -1617 |          -23 |              -1 |                -8 |
| ESPORTSTMNT01_2690219 |             100 |         2114 |          -1763 |         -906 |          -22 |              -2 |                -2 |
| ESPORTSTMNT01_2690227 |             100 |         1972 |           1191 |         2298 |           15 |               2 |                 7 |
| ESPORTSTMNT01_2690255 |             100 |         2488 |            550 |        -1259 |          -40 |               2 |                 6 |
| ESPORTSTMNT01_2690264 |             100 |         2020 |           1478 |          204 |           -9 |               0 |                 4 |


## Univariate Analysis
