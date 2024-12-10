# League of Legends Gamelength Statistical Analysis

League of Legends Gamelength analysis is a data science project exploring the relationship between gamelength and stats. The project includes hypothesis testing, statistical analysis, baseline models, and concludes with fairness analysis. The primary goal for the project is to able to predict the possible gamelength given by the stats differnce between both teams at 25mins. 

Authors: Linus Lee

## General Introduction
League of Legend is a 2009 multiplayer online battle arena video game developed and published by Riot Games. In the game, two teams of five players battle in player-versus-player combat, each team occupying and defending their half of the map. The data set the project will be working on is a professional data set that’s developed by Oracle's Elixir. The file records match data from professional LOL esports gaming matches throughout 2022. 

This dataset captures key gameplay statistics and outcomes from all profession LOL match throughout 2022, offering various features such as individual player performance, champions pick, in-game statistics, and overall match summary.

In the game of League of Legends (LOL), a power of a champion is based on five main category: xp(experience), gold, kills, assists, and cs(minionkills). Xp could help a champion to level up, gold helps a champion to buy items, kills and assists help champion to win advantage and gold in the game, and minionkills are the fundamental of the game to help a player to win gold and control the lanes when fighting against the opponent. If a team can have higher advantage at these five features then the team has higher chance to win the game and end the game sooner. These five features serves as an important feature of a match. 

The central question we are interested in is **Given by the stats difference between both team, are we ablt to predict the game length of the match**. The project is going to use data analysis techniques to testify the impact of five features including xp(experience), gold, kills, assists, and cs(minionkills)). At the end, the project is going to use these statistics and other important feature to set up a prediction model to predict the gamelength of a match.

## Introduction of Columns
The dataset introduces a comprehensive array of columns featuring gameplay metrics and match outcomes from professional League of Legends esports matches. The data set has 150180 rows, and here is an introduction to some of the key columns the project is going to work on:

- 'kills' : The 'kills' column quantifies the number of enemy champions a player or team successfully eliminated during the match. 

- 'assists`: The 'assists' column records the number of assists credited to a player or team, indicating instances where they contributed to eliminating an enemy champion without securing the kill themselves.

- 'xp': The 'xp' column records the total experience a player earn from the start of the game to the end of the game.

- 'gold': The 'gold' column records the total gold a player earn from the start of the game to the end of the game.

- 'minionskill': This column records the number of minions or neutral monsters slain by a player or team during the match. It reflects their ability to efficiently farm gold and experience points, crucial for character progression and itemization.
  
- 'league': The 'league' column denotes the specific league tournament in which the match took place.

- 'patch' : The 'patch' column record the version of the match is playing on.

- `participantid': This column represents a unique identifier for each player and team in a game. It allows us to distinguish each team in a match.

