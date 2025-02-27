# Project overview

The project you just visited focuses on analyzing American basketball played in the NCAA Division I (College) league over the 2013-2023 time span (excluding year 2020 because of covid).
Based on information and statistics provided by the database available on the Kaggle website, research was done on areas of interest and several issues were discussed.
Data taken from https://www.kaggle.com/datasets/andrewsundberg/college-basketball-dataset/data


# The Questions

1. What team/teams were the most-victorious/unsuccesful/mediocre among whole league in 2013-2023?
2. How much influence do the different statistics have on each other?
3. Which team has made the most progress and in what season? What statistics followed?
4. Is the championships won by offense or defense?


# Tools used

- **Python:**
  - **pandas:** for convenient manipulation and analysis of tabular data, such as DataFrames
  - **numpy:** for handling arrays and performing efficient mathematical operations
  - **matplotlib:** for creating aesthetic and transparent plots and data visualizations
  - **seaborn:** for creating even better aesthetic and transparent plots
- **Jupyter Notebooks:** an environment for writing and running Python code
- **Excel:** a spreadsheet application for organizing and analyzing data

# Topics' analysis
As part of the research analysis of this area of knowledge, I focused on using available statistics as much as possible. Because I am interested in this sport, I know what attracts the attention of fans and what conundrums are interesting in this area.
I tried to pose four intriguing questions and extract enough knowledge from the database to make the answers clear and comprehensive.

## 1. What team/teams were the most-victorious/unsuccesful/mediocre among whole league in 2013-2023?
The first issue naturally had to be divided into 3 segments and a different approach was taken to each. In addition to the necessary filtering and cleaning of the data, it was necessary to choose the interpretation according to which the answer would be reached.

### 1.1. Most victorious?
The question of the most winning team has been worked out in two ways:
**The first**, find championship teams and sort them by their number of championships. 
**The second** was to find the teams with the greatest record of winning games (the top 6 were chosen) - to expand the issue, each season was also presented in terms of the number of games won and the results in the playoffs.
With these two approaches, you can additionally juxtapose the teams from the first and second way and check the overlap (interestingly: not necessarily!)

### Results 

![Most championships in 2013-2023](https://github.com/user-attachments/assets/6be1ffca-37c6-4bf2-91f0-ae33a8c4ab17)
*Teams with championships in 2013-2023*

![Most games won in 2013-2023 (top 6)](https://github.com/user-attachments/assets/3d5b499e-52e8-4ecb-af33-ae497f48439c)
*Teams with most games won in 2013-2023 (top 6)*

![Regular season and playoffs for {current_team}](https://github.com/user-attachments/assets/47fd04a6-a214-443b-9dda-5b64f6165a5f)
*Teams with most games won year by year with playoffs results*

### Insights:
- Of the 10 championships won, two teams won the trophy twice. No school has won more. They were Connecticut and Villanova.
- For the top 6 teams with the most wins, only four won the trophy - the championship was not won, with fifth place, Arizona and.
- Gonzaga with a first place finish. The only team to break the 300-win threshold in the 2013-2023 period did not lift the trophy even once.


### 1.2. Most unsuccesful?
The question of the most losing team was simpler and was interpreted as the least winning games in the entire 2013-2023 period - the assumption being that these teams would be among the smallest market, would not be successful in the playoffs, and would not see any “breakthrough” season - after all, there could be a team in this ranking that by some miracle won a championship in one of the seasons, right? But this all became clear after a brief analysis.

### Results 

![Least games won in 2013-2023 (top 6)](https://github.com/user-attachments/assets/25227ec9-4325-47d2-af7a-8ee9c6a1a3c0)
*Teams with least games won in 2013-2023 (top 6)*

![Regular season and playoffs for {current_team}2](https://github.com/user-attachments/assets/3976a6af-1cc0-4db2-b144-432bf2d283a3)
*Teams with least games won year by year with playoffs results*

### Insights:
- Each team represents a not-so-popular school and a weak market, as assumed.
- The lack of a line on the charts showing the outcome of the playoffs is not an error -NONE of the teams made it to the tournament even once. Again, just as assumed.
- There was no breakthrough season, no miracle for any of these teams. Possibly San Jose St. with 21 wins in the 2023 season, which still didn't get them into the playoffs.


### 1.3. Most mediocre?
The issue of the most mediocre/average team is interesting to interpret and can be understood in different ways. 
Successful results did not come from searching for teams by median victory statistics - these teams were successful in one season and low in another. This is certainly not the definition of average!
It was also disappointing to filter and sort teams by how rarely they change their result from season to season - I was able to get a team that got to the playoffs year after year and reached R64 or R32. This is a big no-no!

So some additional features were developed to help identify the “lucky” ones:
- SEED_PRESENT feature, which counted how many times a team made it to the playoffs at all,
- The PROGRESS feature, which tracked how much change (good or bad) occurred from season to season - e.g. from R64 (1) to Championship (7) progress was 6. From Championship to non-playoffs (0)? It amounted to -7,
- The CHANGE_PROGRESS feature, which summed the PROGRESS trait from all years in absolute value, providing how many times and how much the team's result changed at the end of the season.

After that, it was decided to exclude teams with SEED_PRESENT less than 5 (that is, they were left with teams that had taken up the tournament at least 6 seasons out of a possible 10) and sort them by CHANGE_PROGRESS in ascending order - that is, you got those teams whose changes in results from season to season were very small, meaning stagnant.

### Results 

```python
	TEAM	          CHANGE_PROGRESS	PROGRESS	SEED_PRESENT	POSTSEASON_MAP
0	Iona	          4.0             0.0	      6	            6
1	Texas Southern	5.0	            1.0	      7	            7
2	Cincinnati	    5.0	            -1.0	    6	            9
3	Iowa	          7.0	            1.0	      7	            11

```

![Regular season and playoffs for {current_team}3](https://github.com/user-attachments/assets/85688844-7894-49bf-9b41-804abf2a25b9)
*Three most mediocre/average teams year by year with playoffs results*

### Insights:
- The top 3 “average” teams included Iona, Texas Southern and Cincinnati.
- Iona and Cincinnati found themselves in the playoffs tunierju 6 times, yet their total change of position at the end of the regular season was 4 and 5, respectively!
- Texas Southern, with 7 appearances in the playoffs, totaled a value of 5 position changes at the end of the regular season.
- The chart shows how much stagnation and “lack of results” these teams have delivered over the years.
