# Introduction
In the world of competitive gaming, particularly in League of Legends, understanding which roles most significantly impact the outcome of matches is crucial for players, teams, and analysts. Our project, part of the final assessment for the DSC80 course, delves into this question: Which role, ADC (Attack Damage Carry) or Mid Laner, tends to have a more significant impact on the game outcome in matches?

To explore this, we analyzed a comprehensive dataset of League of Legends matches, consisting of more than 15,000 rows. Key columns relevant to our inquiry include:

Role: Indicates the assigned role of the player (e.g., ADC, Mid Laner).
 - Kills: The number of kills a player secures during the match.
 - Deaths: The number of times a player is killed.
 - Assists: The number of assists a player contributes to.
 - Gold Earned: The total amount of gold a player accumulates.
 - Win: A binary indicator showing whether the player's team won the match.
These columns help us measure and compare the performance and impact of ADCs and Mid Laners in determining match outcomes. Readers should care about this analysis as it offers insights into strategic gameplay and role prioritization, which are essential for optimizing team performance and success.

# Data Cleaning and Exploratory Data Analysis
For the sake of this project we will only use the most important columns that are relevant to our research, these are:
| Column Name           | Description                                                                                                                               |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `gameid`              | Unique identifier for each game.                                                                                                          |
| `datacompleteness`    | Indicator of whether the data for the game is complete.                                                                                   |
| `position`            | Player's position in the game (e.g., bot, mid, top, jungle, support).                                                                     |
| `result`              | Outcome of the game for the player (win or loss).                                                                                         |
| `kills`               | Number of kills by the player during the game.                                                                                            |
| `deaths`              | Number of times the player died during the game.                                                                                          |
| `assists`             | Number of assists by the player during the game.                                                                                          |
| `damagetochampions`   | Total damage dealt by the player to enemy champions.                                                                                      |
| `dpm`                 | Damage per minute, indicating how much damage the player deals on average per minute.                                                     |
| `visionscore`         | A score indicating the player's contribution to vision control through wards and vision denial.                                           |
| `golddiffat15`        | Gold difference at 15 minutes compared to the opposing player in the same position.                                                       |
| `csdiffat15`          | Creep score (minion kills) difference at 15 minutes compared to the opposing player in the same position.                                 |
| `killsat15`           | Number of kills by the player at 15 minutes into the game.                                                                                |
| `xpdiffat15`          | Experience difference at 15 minutes compared to the opposing player in the same position.                                                 |
| `firstblood`          | Indicator if the player or their team got the first kill of the game.                                                                     |
| `damageshare`         | Percentage of the team's total damage dealt to champions contributed by the player.                                                       |
| `killsat15`           | Number of kills by the player at 15 minutes into the game. (Repeated to indicate importance in different contexts)                        |
| `assistsat15`         | Number of assists by the player at 15 minutes into the game.                                                                              |
| `deathsat15`          | Number of deaths by the player at 15 minutes into the game.                                                                               |
| `csat15`              | Creep score (minion kills) by the player at 15 minutes into the game.                                                                     |
| `xpat15`              | Experience points gained by the player at 15 minutes into the game.                                                                       |

## Univariate Analysis of Damage Share
