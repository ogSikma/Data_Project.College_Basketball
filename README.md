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

The question of the most winning team has been worked out in two ways:
**The first**, find championship teams and sort them by their number of championships. 
**The second** was to find the teams with the greatest record of winning games (the top 6 were chosen) - to expand the issue, each season was also presented in terms of the number of games won and the results in the playoffs.
With these two approaches, you can additionally juxtapose the teams from the first and second way and check the overlap (interestingly: not necessarily!)
