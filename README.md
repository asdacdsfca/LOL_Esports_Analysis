# LoL Esports Matches Analysis
by Andrew Zhao (yiz158@ucsd.edu)

___
## Introduction to Dataset
- Our data contains the information of **LoL** (League of Legends, a popular moba games) **esports matches** in **2022**.
 - The data is taken from [this website](https://oracleselixir.com/tools/downloads)
 - The question our analysis is investigate on is 
 : 
 
 *Does patch influence the win rate difference between Aphelios and Jinx?*
 - This question is crucial for understanding the **mechanism** of picking characters in LoL professional esports games and the **overall design/fairness** of the game.
 - Here are some of the general statistics about our data:
    - The orignial dataset contains `149232 rows` and `123 columns`
    - The columns that are relevant to our data: 
        - `patch` (Float): contains the information about patch ( patch is similar to a client version. [Click here to read more](https://leagueoflegends.fandom.com/wiki/Patch_(League_of_Legends)#:~:text=A%20patch%20(otherwise%20known%20as,the%20power%20balance%20between%20champions.)).
         - `date` (String): contains the information of the date that a particular match is played.
         - `champion` (String): contains information about the champion that the player picked in a particular game.
         - `result` (Integer): contains information about whether a game is won or lost.

___
## Data Cleaning

**steps**:

1. Clean out the `position` that equals to **team** so we are only looking at the data of **players**
2. We **extract** the **columns** that are needed for furthur investigation
``` 
['patch', 'datacompleteness', 'champion', 'result']
```
3. We observe that `patch` has **missing values** and we observe that `patch` is related to `date`. If the `date` is in a certain range then the missing patch must be the **same** as other games in this range.
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
## Univariate Analysis

<iframe src="Assets/Patch_Probability_Density1.html" width=600 height=600 frameBorder=0></iframe>