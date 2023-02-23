# LoL Esports Matches Analysis
by Andrew Zhao (yiz158@ucsd.edu)

___
## Introduction to Dataset
- Our data contains the information of **LoL** (League of Legends, a popular moba games) **esports matches** in **2022**.
 - The data is taken from [this website](https://oracleselixir.com/tools/downloads)
 - The question our analysis investigates on is 
 : 
 
 *Is Jinx more Likely to Win than Aphelios at any Given Match?*
 - This question is crucial for understanding the **mechanism** of picking characters in LoL professional esports games and the **overall design/fairness** of the game.
 - Here are some of the general statistics about our data:
    - The orignial dataset contains `149232 rows` and `123 columns`
    - The columns that are relevant to our data: 
        - `patch` (Float): contains the information about patch ( patch is similar to a client version. [Click here to read more](https://leagueoflegends.fandom.com/wiki/Patch_(League_of_Legends)#:~:text=A%20patch%20(otherwise%20known%20as,the%20power%20balance%20between%20champions.)). (**!!!Note: We ended up not using this column in our hypothesis test but chose to keep it as it makes our analysis part more smooth**)
         - `date` (String): contains the information of the date that a particular match is played.
         - `champion` (String): contains information about the champion that the player picked in a particular game.
         - `result` (Integer): contains information about whether a game is won or lost.

___
### Data Cleaning

**steps**:

1. Clean out the `position` that equals to **team** so we are only looking at the data of **players**
2. We **extract** the **columns** that are needed for furthur investigation
``` 
['patch', 'datacompleteness', 'champion', 'result']
```
3. We observe that `patch` has **missing values** and through our research we found that `patch` is related to `date`. [Click here to read the official source](https://leagueoflegends.fandom.com/wiki/Patch_(League_of_Legends)#:~:text=A%20patch%20(otherwise%20known%20as,the%20power%20balance%20between%20champions.)). If the `date` is in a certain range then the missing patch must be the **same** as other games in this range. 
4. Now we want to change the **type** of some of the **columns**. The `date` column is now stored as **string** but it makes more sense to have it as **datetime** object. The `result` column is stored as **int64** and we could save memeory if we change it to **bool**

**Here is the first few rows of our cleaned dataframe:**

|   patch | date                | champion   | result   |
|--------:|:--------------------|:-----------|:---------|
|   12.01 | 2022-01-10 07:44:08 | Jinx       | True     |
|   12.01 | 2022-01-10 09:24:26 | Jinx       | True     |
|   12.01 | 2022-01-10 09:24:26 | Aphelios   | False    |
|   12.01 | 2022-01-10 09:51:16 | Aphelios   | True     |
|   12.01 | 2022-01-10 10:09:22 | Jinx       | True     |

___
### Univariate Analysis

<iframe src="Assets/champ.html" width=600 height=600 frameBorder=0></iframe>

**Exaplantion**:
We observe that the **Jinx** has lower pick rate than **Aphelios**.  

___
### Bivariate Analysis

<iframe src="Assets/date_character.html" width=600 height=600 frameBorder=0></iframe>

**Exaplantion**:
We observe that the number of games each chacter appears is distributed differently throughout the year. Some date intervals have more games that have `Jinx` and `Aphelios` and some contain less. For example `February` has significantly more games that contain `Jinx` and `Aphelios` than `December`. Another observation is that in some month `Aphelios` appeared in more games than `Jinx` and vise versa. 

<iframe src="Assets/result_champ.html" width=600 height=600 frameBorder=0></iframe>

**Exaplantion**:
We observe that `Jinx` has a slightly higher **overall** win rate than `Aphelios` at any given match. This observation leads us to think: **Is Jinx more Likely to Win than Aphelios at any Given Match?** which is essentially what the anlysis is about. 

___
### Interesting Aggregates

|   patch | champion   |   result |
|--------:|:-----------|---------:|
|   12.01 | Aphelios   | 0.49375  |
|   12.01 | Jinx       | 0.542453 |
|   12.02 | Aphelios   | 0.478723 |
|   12.02 | Jinx       | 0.505455 |
|   12.03 | Aphelios   | 0.473002 |
|   12.03 | Jinx       | 0.530055 |
|   12.04 | Aphelios   | 0.480328 |
|   12.04 | Jinx       | 0.537805 |
|   12.05 | Aphelios   | 0.495475 |
|   12.05 | Jinx       | 0.5      |
|   12.06 | Aphelios   | 0.5      |
|   12.06 | Jinx       | 0.521739 |
|   12.07 | Aphelios   | 0.6875   |
|   12.07 | Jinx       | 0.575    |
|   12.08 | Aphelios   | 0.352941 |
|   12.08 | Jinx       | 0.333333 |
|   12.09 | Aphelios   | 0.434783 |
|   12.09 | Jinx       | 0.432432 |
|   12.1  | Aphelios   | 0.6      |
|   12.1  | Jinx       | 0.478992 |
|   12.11 | Aphelios   | 0.568047 |
|   12.11 | Jinx       | 0.398438 |
|   12.12 | Aphelios   | 0.508642 |
|   12.12 | Jinx       | 0.395833 |
|   12.13 | Aphelios   | 0.478022 |
|   12.13 | Jinx       | 0.48     |
|   12.14 | Aphelios   | 0.459184 |
|   12.14 | Jinx       | 0.387755 |
|   12.15 | Aphelios   | 0.57265  |
|   12.15 | Jinx       | 0.428571 |
|   12.16 | Aphelios   | 0.433962 |
|   12.16 | Jinx       | 0.5      |
|   12.17 | Aphelios   | 1        |
|   12.17 | Jinx       | 0.333333 |
|   12.18 | Aphelios   | 0.526316 |
|   12.18 | Jinx       | 0.346154 |
|   12.19 | Aphelios   | 0.363636 |
|   12.19 | Jinx       | 0.545455 |
|   12.2  | Aphelios   | 0.46875  |
|   12.2  | Jinx       | 0.4      |
|   12.21 | Aphelios   | 0.4375   |
|   12.21 | Jinx       | 0.2      |
|   12.23 | Aphelios   | 0.25     |
|   12.23 | Jinx       | 1        |

**Exaplantion**:
This grouped table shows the win rate of `Jinx` and `Aphelios` individually by `patch`. Though this is not closely related to our anlysis question, however, this leads us to think of an interesting question: **Does patch influence the win rate difference between Jinx and Aphelios?**. Some idea we have in mind would be performing an `ANOVA` F-test, though we are not going to explore this topic on this project.

___
## Assessment of Missingness


___
## Hypothesis Testing
**Null Hypothesis:**
In the population, win rate of `Jinx` and `Aphelios` at any given match have the same distribution, and the observed differences in our samples are due to random chance.

**Alternative Hypothesis:**
In the population, `Jinx` has higher win rate than `Aphelios` at any given match, on average. The observed difference in our samples cannot be explained by random chance alone.