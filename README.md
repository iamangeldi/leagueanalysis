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


| Column Name         | Description                                                                                                         |
|---------------------|---------------------------------------------------------------------------------------------------------------------|
| `gameid`            | Unique identifier for each game.                                                                                   |
| `datacompleteness`  | Indicator of whether the data for the game is complete.                                                            |
| `position`          | Player's position in the game (e.g., bot, mid, top, jungle, support).                                              |
| `result`            | Outcome of the game for the player (win or loss).                                                                  |
| `kills`             | Number of kills by the player during the game.                                                                     |
| `deaths`            | Number of times the player died during the game.                                                                   |
| `assists`           | Number of assists by the player during the game.                                                                   |
| `damagetochampions` | Total damage dealt by the player to enemy champions.                                                               |
| `dpm`               | Damage per minute, indicating how much damage the player deals on average per minute.                              |
| `visionscore`       | A score indicating the player's contribution to vision control through wards and vision denial.                    |
| `golddiffat15`      | Gold difference at 15 minutes compared to the opposing player in the same position.                                |
| `csdiffat15`        | Creep score (minion kills) difference at 15 minutes compared to the opposing player in the same position.          |
| `killsat15`         | Number of kills by the player at 15 minutes into the game.                                                         |
| `xpdiffat15`        | Experience difference at 15 minutes compared to the opposing player in the same position.                          |
| `firstblood`        | Indicator if the player or their team got the first kill of the game.                                              |
| `damageshare`       | Percentage of the team's total damage dealt to champions contributed by the player.                                |
| `killsat15`         | Number of kills by the player at 15 minutes into the game. (Repeated to indicate importance in different contexts) |
| `assistsat15`       | Number of assists by the player at 15 minutes into the game.                                                       |
| `deathsat15`        | Number of deaths by the player at 15 minutes into the game.                                                        |
| `csat15`            | Creep score (minion kills) by the player at 15 minutes into the game.                                              |
| `xpat15`            | Experience points gained by the player at 15 minutes into the game.                                                |

## Univariate Analysis of Damage Share
![Univariate Analysis](assets/univariative_analysis.png)

The histogram depicts the distribution of damageshare among players in a League of Legends dataset, showing how much each player contributes to their team's total damage dealt to champions. Most players fall within the 10% to 30% range, indicating a common spread where individual contributions are significant but balanced. The sharp decline beyond 30% suggests fewer players are heavily skewed towards dominating their team's damage output, likely highlighting roles such as ADCs or mid-laners who are primary damage dealers. This distribution reflects typical team dynamics where damage is moderately shared among key roles, ensuring versatility and resilience in gameplay.

## Bivariate Analysis between position and damage share
![Bivariate Analysis](assets/bivariative_analysis.png)

This box plot illustrates the damageshare distribution across different positions in League of Legends: top, jungle (jng), mid, bot, and support (sup). The mid and bot positions show higher median damageshare, around 0.25, indicating they often contribute significantly to the team's total damage. The jungle position typically has a lower median damageshare near 0.15, reflecting their broader role in map control and objective play rather than direct damage dealing. Supports have the lowest median damageshare and a narrower range, focusing more on utility and protection than damage output. The top lane position displays a moderate damageshare, with a median around 0.20, highlighting a balanced role between damage and tanking or split-pushing. This plot underscores the distinct roles and expected damage contributions of each position within a team.

## Instresting aggregates and pivots
In order to get a full understanding of the data we are given lets work with a few pivots, this will help us get a better understanding of the game, and might lead us to future projects.

| Position | Assists | Damage Share | Deaths | Kills | Total Gold |
|----------|---------|--------------|--------|-------|------------|
| bot      | 5.60    | 0.27         | 2.58   | 4.51  | 13876.32   |
| jng      | 7.82    | 0.14         | 3.14   | 2.56  | 10916.34   |
| mid      | 6.20    | 0.28         | 2.61   | 3.69  | 13301.80   |
| sup      | 9.75    | 0.09         | 3.33   | 0.91  | 8372.47    |
| top      | 5.06    | 0.23         | 2.87   | 2.82  | 12532.96   |


# Assessment of Missingness
In this step, we're investigating the missing values in the `xpdiffat15` column of our League of Legends dataset. The idea is to determine if the missingness is systematically related to other gameplay metrics, which could suggest that the missing data is not random (potentially Missing Not at Random, or MNAR). We create a new column xpdiffat15_missing to flag the missing values. Then, we perform permutation tests on various columns (kills, deaths, assists, and totalgold) to see if there's a significant difference in their means between games with and without missing xpdiffat15. This involves shuffling the data and comparing the observed differences with these random permutations to compute p-values, helping us understand if the observed differences are statistically significant or likely due to chance.

## Permutation test with 'xpdiffat15' and 'kills' columns
***Null Hypothesis (H0):*** The missingness of xpdiffat15 is independent of the kills column. In other words, any observed difference in means between the missing and non-missing groups for xpdiffat15 is due to random chance.

***Alternative Hypothesis (H1):*** The missingness of xpdiffat15 is dependent on the kills column. This means that the observed difference in means between the missing and non-missing groups for xpdiffat15 is not due to random chance and indicates a significant relationship between the two variables.

![Permutation Test for Kills](assets/permutation_kills.png)

The histogram represents the distribution of the difference in means obtained from the permutation tests, illustrating the null hypothesis that there's no relationship between the missingness of xpdiffat15 and kills. The red dashed line indicates the actual observed difference in means, and its position outside the bulk of the distribution suggests a significant dependency between these variables. This implies that the observed difference is unlikely to have occurred by chance, confirming a significant relationship.

## Permutation test with 'xpdiffat15' and 'totalgold' columns
***Null Hypothesis (H0):*** The missingness of xpdiffat15 is independent of the totalgold column. Any observed difference in means between the missing and non-missing groups for xpdiffat15 is due to random chance.

***Alternative Hypothesis (H1):*** The missingness of xpdiffat15 is dependent on the totalgold column. The observed difference in means between the missing and non-missing groups for xpdiffat15 is not due to random chance and indicates a significant relationship.
![Permutation Test for Kills](assets/permutation_total_gold.png)

The histogram represents the distribution of the difference in means obtained from the permutation tests, illustrating the null hypothesis that there's no relationship between the missingness of xpdiffat15 and totalgold. The red dashed line indicates the actual observed difference in means, and its position outside the bulk of the distribution suggests a significant dependency between these variables. This implies that the observed difference is unlikely to have occurred by chance, confirming a significant relationship.

# Hypothesis Testing


