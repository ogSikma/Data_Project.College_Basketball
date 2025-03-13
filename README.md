# Project overview

The project you just visited focuses on analyzing American basketball played in the NCAA Division I (College) league over the 2013-2023 time span (excluding year 2020 because of covid).
Based on information and statistics provided by the database available on the Kaggle website, research was done on areas of interest and several issues were discussed. <br>
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
As part of the research analysis of this area of knowledge, I focused on using available statistics as much as possible. Because I am interested in this sport, I know what attracts the attention of fans and what conundrums are interesting in this area. <br>
I tried to pose four intriguing questions and extract enough knowledge from the database to make the answers clear and comprehensive.


## 1. What team/teams were the most-victorious/unsuccesful/mediocre among whole league in 2013-2023?
The first issue naturally had to be divided into 3 segments and a different approach was taken to each. In addition to the necessary filtering and cleaning of the data, it was necessary to choose the interpretation according to which the answer would be reached.
<br><br>

### 1.1. Most victorious?
The question of the most winning team has been worked out in two ways: <br>
**The first**, find championship teams and sort them by their number of championships. <br>
**The second** was to find the teams with the greatest record of winning games (the top 6 were chosen) - to expand the issue, each season was also presented in terms of the number of games won and the results in the playoffs. <br><br>
With these two approaches, you can additionally juxtapose the teams from the first and second way and check the overlap (interestingly: not necessarily!)

### Results 

![Most championships in 2013-2023](https://github.com/user-attachments/assets/6be1ffca-37c6-4bf2-91f0-ae33a8c4ab17) <br>
*Teams with championships in 2013-2023*

![Most games won in 2013-2023 (top 6)](https://github.com/user-attachments/assets/3d5b499e-52e8-4ecb-af33-ae497f48439c) <br>
*Teams with most games won in 2013-2023 (top 6)*

![Regular season and playoffs for {current_team}](https://github.com/user-attachments/assets/47fd04a6-a214-443b-9dda-5b64f6165a5f) <br>
*Teams with most games won year by year with playoffs results*

### Insights:
- Of the 10 championships won, two teams won the trophy twice. No school has won more. They were Connecticut and Villanova.
- For the top 6 teams with the most wins, only four won the trophy - the championship was not won, with fifth place, Arizona and.
- Gonzaga with a first place finish. The only team to break the 300-win threshold in the 2013-2023 period did not lift the trophy even once.
<br><br>

### 1.2. Most unsuccesful?
The question of the most losing team was simpler and was interpreted as the least winning games in the entire 2013-2023 period. <br>
The assumption being that these teams would be among the smallest market, would not be successful in the playoffs, and would not see any “breakthrough” season - after all, there could be a team in this ranking that by some miracle won a championship in one of the seasons, right? <br><br>
But this all became clear after a brief analysis.

### Results 

![Least games won in 2013-2023 (top 6)](https://github.com/user-attachments/assets/25227ec9-4325-47d2-af7a-8ee9c6a1a3c0) <br>
*Teams with least games won in 2013-2023 (top 6)*

![Regular season and playoffs for {current_team}2](https://github.com/user-attachments/assets/3976a6af-1cc0-4db2-b144-432bf2d283a3) <br>
*Teams with least games won year by year with playoffs results*

### Insights:
- Each team represents a not-so-popular school and a weak market, as assumed.
- The lack of a line on the charts showing the outcome of the playoffs is not an error -NONE of the teams made it to the tournament even once. Again, just as assumed.
- There was no breakthrough season, no miracle for any of these teams. Possibly San Jose St. with 21 wins in the 2023 season, which still didn't get them into the playoffs.
<br><br>

### 1.3. Most mediocre?
The issue of the most mediocre/average team is interesting to interpret and can be understood in different ways. <br>
Successful results did not come from searching for teams by median victory statistics - these teams were successful in one season and low in another. This is certainly not the definition of average! <br>
It was also disappointing to filter and sort teams by how rarely they change their result from season to season - I was able to get a team that got to the playoffs year after year and reached R64 or R32. This is a big no-no! <br>

So some additional features were developed to help identify the “lucky” ones:
- SEED_PRESENT feature, which counted how many times a team made it to the playoffs at all,
- The PROGRESS feature, which tracked how much change (good or bad) occurred from season to season - e.g. from R64 (1) to Championship (7) progress was 6. From Championship to non-playoffs (0)? It amounted to -7,
- The CHANGE_PROGRESS feature, which summed the PROGRESS trait from all years in absolute value, providing how many times and how much the team's result changed at the end of the season.
<br><br>
After that, it was decided to exclude teams with SEED_PRESENT less than 5 (that is, they were left with teams that had taken up the tournament at least 6 seasons out of a possible 10) and sort them by CHANGE_PROGRESS in ascending order - that is, you got those teams whose changes in results from season to season were very small, meaning stagnant.

### Results 

```python
	TEAM	          CHANGE_PROGRESS	PROGRESS	SEED_PRESENT	POSTSEASON_MAP
0	Iona	          4.0            	0.0	    	6	        6
1	Texas Southern	  5.0	           	1.0	   	7	        7
2	Cincinnati	  5.0	         	-1.0	    	6	        9
3	Iowa	          7.0	          	1.0	    	7	        11

```

![Regular season and playoffs for {current_team}3](https://github.com/user-attachments/assets/85688844-7894-49bf-9b41-804abf2a25b9)
*Three most mediocre/average teams year by year with playoffs results*

### Insights:
- The top 3 “average” teams included Iona, Texas Southern and Cincinnati.
- Iona and Cincinnati found themselves in the playoffs tunierju 6 times, yet their total change of position at the end of the regular season was 4 and 5, respectively!
- Texas Southern, with 7 appearances in the playoffs, totaled a value of 5 position changes at the end of the regular season.
- The chart shows how much stagnation and “lack of results” these teams have delivered over the years.
<br><br>

## 2. How much influence do the different statistics have on each other?
Analyzing the correlation between statistics and the influence of one characteristic on another positively or negatively is easiest with a heat map, and this is how it was done.

### Results 

![Corelations between features](https://github.com/user-attachments/assets/8fe3e8e5-82f6-42c0-abaa-d5a98a527314)
*Corelations between features on heatmap*

### Insights:
1. **SEED**
- For a higher place at the end of the regular season, the high influence (as you might guess) is winning games [W] with a score of -0.54.
- Of the less obvious ones, [BARTHAG] (-0.83) and [ADJDE] (0.69) along with [ADJOE] (-0.74) have the greatest impact.
- Interesting item is the number of games [G] with a score of -0.36, which means that the fewer games played the higher (worse) the seed at the end of the season.
<br><br>
2. **YEAR**
- The feature concerning time [YEAR] had a slight, but nevertheless, influence on the number of games [G] - decreasingly.
- Its effect on the features relating to 2-point throws - [2P_O] and [2P_D] - is evident, and with both having a value of 0.23.
- Most interesting is the decrease in free throws represented by the [FTR] and [FTRD] traits (-0.48 and -0.41)- the [YEAR] trait has a large, negative, impact, which means a decreasing number of free throws in matches.
<br><br>
3. **WON GAMES**
- The overall, aggregate number of games won [W] correlates strongly or significantly with a number of features - whether statistics relating to offensive and defensive efficiency ([ADJOE] and [ADJDE]), or shooting efficiency [EFG_O] etc. But what has the weakest correlation, that is, has the least impact on each other?
- Certainly the number of free throws: made by one's own team [FTR] (0.16) and made by the opponent [FTRD] (-0.26). Ball losses committed by the opponent (steals by one's own team), also have a weak impact: [TORD] (0.14), although one's own ball losses have a large impact: [TOR] (-0.44).
<br>

**For more notes and details visit the file dedicated to this analysis!**


## 3. Which team has made the most progress and in what season? What statistics followed?
A couple of new features were needed to analyze this question. <br>
**First**, it was necessary to map the column containing the result in the playoffs to numbers so that the program could operate on them more easily. <br>
**Next**, a second feature was created containing progress and which referred to the progress made relative to the previous season. The teams could then be sorted according to the greatest progression.<br>

```python
for team in team_list:
    df_team = df_all_years[df_all_years['TEAM'] == team]
    for year in df_team['YEAR'].iloc[1:]:
        if year == 2021:
            progress = (df_team.loc[df_team['YEAR'] == year, 'POSTSEASON_MAP'].iloc[0]) - (df_team.loc[df_team['YEAR'] == year-2, 'POSTSEASON_MAP'].iloc[0])
        else:
            progress = (df_team.loc[df_team['YEAR'] == year, 'POSTSEASON_MAP'].iloc[0]) - (df_team.loc[df_team['YEAR'] == year-1, 'POSTSEASON_MAP'].iloc[0])
        df_all_years_progress = add_row(year, team, progress, df_all_years_progress)
```
**team_list** contains unique teams' names and with each iteration in loop we analyse progress of one team made year by year. How? <br>
For every year from 2013 to 2023 we are checking how the **POSTSEASON_MAP** (playoffs result as number) changed and that means we subtract the value of the current year from the previous year. <br>
Important: in 2021 we refer to 2019, as there were no games in 2020 (covid)

### Results 

```python
	TEAM		YEAR	POSTSEASON_MAP	PROGRESS
0	Connecticut	2014	7		7.0
1	Kentucky	2014	6		6.0
2	Virginia	2019	7		6.0
3	Duke		2015	7		6.0
4	Connecticut	2023	7		6.0
5	San Diego St.	2023	6		5.0

```

### Insights:
- As you can see, one team made a huge success in 2014 relative to 2013 (progress=7): Connecticut from a lack of performance in the playoffs reached the championship.
- This is the only such case, below Connecticut there were 4 teams with progress equal to 6.
- Among these four teams, as many as three of them jumped from the first round of the R64 playoffs to the championship: Virginia, Duke and... Connecticut again!

### Stats visualization
But the question included what statistics have followed such tremendous progress? To show this we will choose the team from the first place in the table, Connecticut and, for example, Virginia from the third place.

![Connecticut](https://github.com/user-attachments/assets/7c3fbb5f-96a8-4af7-a4d8-c1b8c81151fb)
*Connecticut stats in championship year 2014 in comparison to 2013*

![Virginia](https://github.com/user-attachments/assets/09ddd873-1b82-4c5f-a7c1-4f10db5d7f79)
*Virginia stats in championship year 2019 in comparison to 2018*
<br><br>

## 4. Is the championships won by offense or defense?
Ah, yes. The eternal conundrum, the fight, the verbal tussle. <br>
Can a hole in the defense be patched up with a fast and aggressive attack? <br>
Can a sluggish offensive be covered up by a tough and thoughtful defense?<br>
<br><br>
The set of statistics I've been working on doesn't go that deep into this area - in fact, the database really offers a lot of data, but superficial. <br>
But working with what I had I visualized the relevant data to shed some light on the matter.<br>

I divided the actual dataframe into separate dataframes, which I grouped by:
- all teams
- teams **without** advance to the playoffs
- teams **with** advance to the playoffs
- championship teams
I then presented on line graphs the ADJDE and ADJOE metrics, which are ratings of defensive and offensive efficiency. <br><br>
In separate charts, I presented the percentage difference between championship teams and teams with advance to the playoffs.

### Results 

![OffenseOrDefense](https://github.com/user-attachments/assets/d341636e-e521-43a2-a14f-64ddec3ca821)
*ADJOE and ADJDE between teams*

### Insights:
- Best offensive of the championship team? **2018 Villanova**. An offensive metric as high as 128.4! 15% more than the rest of the teams in the playoffs. The worst offensive? **2014 Connecticut**, only 112.5. managed to fit with a score 0.14% better than the average of playoff teams. And this allowed the following conclusion:
- in every year, the champion team had a better offensive performance than the playoff average. Barely!
- Best defense? **2013 Louisville**, with a defensive metric of 84.5 - 10% better than the average of playoff teams! Worst defense? **2021 Baylor** with a score of 94.5. Poor, less than 1% better than the average of playoff teams....
- ...but it's also fair to say that every championship team had a better defensive performance. Barely x2!
- Summary, the bigger differences between the championship teams and the rest can be seen in offense - the defense is more similar to other teams, especially the playoff teams, but it's still outclassed. Still, minimally it is the offense that stands out more, **so one can conclude from this data that the offense is more important**.


# Want more?
I encourage you to check the notebook for each issue for a detailed breakdown of the tasks and more details.

# Tableau
I also invite you to see my visualization of college basketball on my Tableau profile: <br>
**https://public.tableau.com/views/NCAAbasketball2013-2023/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link**

