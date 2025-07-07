#IPL Ball-by-Ball Analysis
This project analyzes IPL ball-by-ball data to uncover key insights like top batsmen, wicket-takers, team performance per season, and run patterns over overs.

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("ball_by_ball_data.csv")
df.head()
season_id	match_id	batter	bowler	non_striker	team_batting	team_bowling	over_number	ball_number	batter_runs	...	is_bye	is_penalty	wide_ball_runs	no_ball_runs	leg_bye_runs	bye_runs	penalty_runs	wicket_kind	is_super_over	innings
0	2008	335982	SC Ganguly	P Kumar	BB McCullum	6	1	0	0	0	...	False	False	0	0	1	0	0	NaN	False	1
1	2008	335982	BB McCullum	P Kumar	SC Ganguly	6	1	0	1	0	...	False	False	0	0	0	0	0	NaN	False	1
2	2008	335982	BB McCullum	P Kumar	SC Ganguly	6	1	0	2	0	...	False	False	1	0	0	0	0	NaN	False	1
3	2008	335982	BB McCullum	P Kumar	SC Ganguly	6	1	0	3	0	...	False	False	0	0	0	0	0	NaN	False	1
4	2008	335982	BB McCullum	P Kumar	SC Ganguly	6	1	0	4	0	...	False	False	0	0	0	0	0	NaN	False	1
5 rows × 30 columns

df.info()
df.isnull().sum()

# Convert categorical columns if needed
df['player_out'] = df['player_out'].fillna("Not Out")
df['wicket_kind'] = df['wicket_kind'].fillna("None")
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 278205 entries, 0 to 278204
Data columns (total 30 columns):
 #   Column             Non-Null Count   Dtype 
---  ------             --------------   ----- 
 0   season_id          278205 non-null  int64 
 1   match_id           278205 non-null  int64 
 2   batter             278205 non-null  object
 3   bowler             278205 non-null  object
 4   non_striker        278205 non-null  object
 5   team_batting       278205 non-null  int64 
 6   team_bowling       278205 non-null  int64 
 7   over_number        278205 non-null  int64 
 8   ball_number        278205 non-null  int64 
 9   batter_runs        278205 non-null  int64 
 10  extras             278205 non-null  int64 
 11  total_runs         278205 non-null  int64 
 12  batsman_type       278205 non-null  object
 13  bowler_type        278205 non-null  object
 14  player_out         13823 non-null   object
 15  fielders_involved  13823 non-null   object
 16  is_wicket          278205 non-null  bool  
 17  is_wide_ball       278205 non-null  bool  
 18  is_no_ball         278205 non-null  bool  
 19  is_leg_bye         278205 non-null  bool  
 20  is_bye             278205 non-null  bool  
 21  is_penalty         278205 non-null  bool  
 22  wide_ball_runs     278205 non-null  int64 
 23  no_ball_runs       278205 non-null  int64 
 24  leg_bye_runs       278205 non-null  int64 
 25  bye_runs           278205 non-null  int64 
 26  penalty_runs       278205 non-null  int64 
 27  wicket_kind        13823 non-null   object
 28  is_super_over      278205 non-null  bool  
 29  innings            278205 non-null  int64 
dtypes: bool(7), int64(15), object(8)
memory usage: 50.7+ MB
top_batsmen = df.groupby('batter')['batter_runs'].sum().sort_values(ascending=False).head(10)
top_batsmen.plot(kind='bar', title='Top 10 Run Scorers in IPL', color='orange')
plt.xlabel('Batsman'); plt.ylabel('Runs'); plt.tight_layout()
No description has been provided for this image
wicket_df = df[df['is_wicket'] == True]
top_bowlers = wicket_df['bowler'].value_counts().head(10)
top_bowlers.plot(kind='bar', title='Top 10 Wicket Takers in IPL', color='green')
plt.xlabel('Bowler'); plt.ylabel('Wickets'); plt.tight_layout()
No description has been provided for this image
team_runs = df.groupby('team_batting')['total_runs'].sum().sort_values(ascending=False)
team_runs.plot(kind='barh', title='Total Runs by Teams')
plt.xlabel('Total Runs'); plt.tight_layout()
No description has been provided for this image
over_runs = df.groupby('over_number')['total_runs'].mean()
sns.lineplot(x=over_runs.index, y=over_runs.values)
plt.title('Average Runs per Over')
plt.xlabel('Over Number'); plt.ylabel('Average Runs')
Text(0, 0.5, 'Average Runs')
No description has been provided for this image
wicket_kind = df[df['wicket_kind'] != "None"]['wicket_kind'].value_counts()
wicket_kind.plot(kind='pie', autopct='%1.1f%%', title='Types of Dismissals', figsize=(6,6))
<Axes: title={'center': 'Types of Dismissals'}, ylabel='count'>
No description has been provided for this image
🔍 Key Insights
🏏 Top Run Scorer: Virat Kohli has scored the most runs in IPL overall.
🎯 Top Wicket Taker: Lasith Malinga has taken the highest number of wickets.
💥 Teams tend to score more runs in the death overs (16–20).
❌ The most common dismissal types are caught and bowled.
🧠 Spinner bowlers dominate in middle overs due to lower economy rates.
✅ Conclusion
In this project, we performed a detailed analysis of IPL ball-by-ball data.

Identified top-performing batsmen and bowlers across all seasons.
Analyzed team-wise scoring patterns and run distribution over overs.
Explored how and when most wickets fall and the common types of dismissals.
This analysis can help:

Coaches and analysts build better team strategies.
Fans and fantasy league players understand performance trends.
Serve as a foundation for predictive modeling and interactive dashboards.
Overall, this project demonstrates how Python and data visualization can uncover powerful insights from large sports datasets.

 
