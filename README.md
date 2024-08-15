# Analyzing European Football Player's Stats 
### A Data Science Project Proposal

#### **Contributors** : `Noam David` - 314803628, `Yaniv Simmer` - 206328817
<br>


## Preface
The football economy is blooming. Players are bought by European clubs for tens of millions of dollars every year.<br>
Also, in the recent years, football went through a major data revolution. Every little action that a player does is measured and well documented, leading to an efficient tool for analyzing a player's performance.<br>
We chose to use some of this data to try to predict a player's value according to the data collected about him.

<br>
<br>

## Research Question
Our research will focus on predicting a player's value by the data collected on him that season.<br>
The German website [Transfermarkt](https://www.transfermarkt.com/) is the leading source for evaluating a player's value, we will use their valuations as the target variable to test our predictions.<br>
We will rely on the data gathered by [FBref.com](https://fbref.com/) (Football Reference), the attributes are age, average minutes per game, goals, shots on goal, interceptions, distance covered etc.<br>
Full description on the attributes is added as an appendix.<br>
We assume that the attributes relevant to a player differ by his position, for example the goals scored by the player are not relevant if the player is a goalkeeper, but they sure are meaningful if he is a striker.<br>
Because of that we will build a different prediction model for every position.

<br>
<br>

## Dataset
### kaggle raw data folder
We use two different datasets, both are from Kaggle.<br>

For the players stats we use a dataset which contains data about players from the top 5 leagues in Europe (England, Spain, France, Italy and Germany).
We have two of those, one for the season 2021/22, and one for 2022/23.
- `2021-2022-football-player-stats.csv` - [Link](https://www.kaggle.com/datasets/vivovinco/20212022-football-player-stats)
- `2022-2023-football-player-stats.csv` - [Link](https://www.kaggle.com/datasets/vivovinco/20222023-football-player-stats)

Each of them has more than 2500 rows(players) and between 143-124 columns of attributes specified in the appendix.

For the player's price valuation, we use this dataset:
- `player-scores-prices.csv` - [Link](https://www.kaggle.com/datasets/davidcariboo/player-scores)


It is an updating dataset, we are using two of the CSV's in it.<br>
One has a matching between a player and the player's id and position, the other has market valuations for every player id in different dates.<br>
We combined those datasets to 7 CSV's, each for every player position.
In every table, each row represents a player in one of the seasons, and has as columns all of the numerical attributes (115) and the market value that season which is the target column.<br>
The positions chosen are: Goalkeeper, Left/Right back, Center back, Defensive midfielder, Attacking midfielder, Left/Right wing and Center forward. 

- `players.csv` - [Link](https://www.kaggle.com/datasets/davidcariboo/player-scores?select=players.csv) (this file is just for indexing players names to their id)


### processed data folder
In this folder there is a file for each position with 115 columns ready for cleaning and begining the project.
- `combined.csv` - 3787 (all positions) 
- `Back_players.csv` - 611 rows
- `Centre-Back_players.csv` - 666 rows
- `Defensive Midfield_players.csv` - 832 rows
- `Centre-Forward_players.csv` - 574 rows
- `Winger_players.csv` - 536 rows
- `Goalkeeper_players.csv` - 253 rows
- `Attacking Midfield_players.csv` - 314 rows

Here's the ChatGPT conversation that helped to write the code in `extract_data.py` - [Link](https://chatgpt.com/share/4e31e197-c0f5-4f90-b2b0-27f1d4f59815)
<br>
<br>


## Methods:
We will start with exploratory data analysis, in which we will look for missing values and columns that do not look right by plotting the data and comparing the min/max values to the mean and standard deviation, while saving 20% of the data for testing.<br>
Then we will perform PCA to reduce dimensions by looking for correlating variables and observing at the variables factor map.<br>
We will fit a regression model for every position to predict the market value of the player that season using cross-validation.<br>
To make sure our prediction is good enough, we will consider the R2, and compare our predictions on the test cases with the actual market value and look at the error.<br>
Finally, we will look for the most contributing variables to predict the market value, by looking at the p-values.


<br>
<br>



## Getting Started

To get started with the project, clone the repository and install the required dependencies:

```bash
git clone https://github.com/yaniv-simmer/data-science-project.git
cd football-stats-analysis
```
<br>
<br>

## Appendix: 
Columns' descriptions are listed below.
- Rk : Rank
- Player : Player's name
- Nation : Player's nation
- Pos : Position
- Squad : Squad’s name
- Comp : League that squat occupies
- Age : Player's age
- Born : Year of birth
- MP : Matches played
- Starts : Matches started
- Min : Minutes played
- 90s : Minutes played divided by 90
- Goals : Goals scored or allowed
- Shots : Shots total (Does not include penalty kicks)
- SoT : Shots on target (Does not include penalty kicks)
- SoT% : Shots on target percentage (Does not include penalty kicks)
- G/Sh : Goals per shot
- G/SoT : Goals per shot on target (Does not include penalty kicks)
- ShoDist : Average distance, in yards, from goal of all shots taken (Does not include penalty kicks)
- ShoFK : Shots from free kicks
- ShoPK : Penalty kicks made
- PKatt : Penalty kicks attempted
- PasTotCmp : Passes completed
- PasTotAtt : Passes attempted
- PasTotCmp% : Pass completion percentage
- PasTotDist : Total distance, in yards, that completed passes have traveled in any direction
- PasTotPrgDist : Total distance, in yards, that completed passes have traveled towards the opponent's goal
- PasShoCmp : Passes completed (Passes between 5 and 15 yards)
- PasShoAtt : Passes attempted (Passes between 5 and 15 yards)
- PasShoCmp% : Pass completion percentage (Passes between 5 and 15 yards)
- PasMedCmp : Passes completed (Passes between 15 and 30 yards)
- PasMedAtt : Passes attempted (Passes between 15 and 30 yards)
- PasMedCmp% : Pass completion percentage (Passes between 15 and 30 yards)
- PasLonCmp : Passes completed (Passes longer than 30 yards)
- PasLonAtt : Passes attempted (Passes longer than 30 yards)
- PasLonCmp% : Pass completion percentage (Passes longer than 30 yards)
- Assists : Assists
- PasAss : Passes that directly lead to a shot (assisted shots)
- Pas3rd : Completed passes that enter the 1/3 of the pitch closest to the goal
- PPA : Completed passes into the 18-yard box
- CrsPA : Completed crosses into the 18-yard box
- PasProg : Completed passes that move the ball towards the opponent's goal at least 10 yards from its furthest point in the last six passes, or any completed pass into the penalty area
- PasAtt : Passes attempted
- PasLive : Live-ball passes
- PasDead : Dead-ball passes
- PasFK : Passes attempted from free kicks
- TB : Completed pass sent between back defenders into open space
- Sw : Passes that travel more than 40 yards of the width of the pitch
- PasCrs : Crosses
- TI : Throw-Ins taken
- CK : Corner kicks
- CkIn : Inswinging corner kicks
- CkOut : Outswinging corner kicks
- CkStr : Straight corner kicks
- PasCmp : Passes completed
- PasOff : Offsides
- PasBlocks : Blocked by the opponent who was standing it the path
- SCA : Shot-creating actions
- ScaPassLive : Completed live-ball passes that lead to a shot attempt
- ScaPassDead : Completed dead-ball passes that lead to a shot attempt
- ScaDrib : Successful dribbles that lead to a shot attempt
- ScaSh : Shots that lead to another shot attempt
- ScaFld : Fouls drawn that lead to a shot attempt
- ScaDef : Defensive actions that lead to a shot attempt
- GCA : Goal-creating actions
- GcaPassLive : Completed live-ball passes that lead to a goal
- GcaPassDead : Completed dead-ball passes that lead to a goal
- GcaDrib : Successful dribbles that lead to a goal
- GcaSh : Shots that lead to another goal-scoring shot
- GcaFld : Fouls drawn that lead to a goal
- GcaDef : Defensive actions that lead to a goal
- Tkl : Number of players tackled
- TklWon : Tackles in which the tackler's team won possession of the ball
- TklDef3rd : Tackles in defensive 1/3
- TklMid3rd : Tackles in middle 1/3
- TklAtt3rd : Tackles in attacking 1/3
- TklDri : Number of dribblers tackled
- TklDriAtt : Number of times dribbled past plus number of tackles
- TklDri% : Percentage of dribblers tackled
- TklDriPast : Number of times dribbled past by an opposing player
- Blocks : Number of times blocking the ball by standing in its path
- BlkSh : Number of times blocking a shot by standing in its path
- BlkPass : Number of times blocking a pass by standing in its path
- Int : Interceptions
- Tkl+Int : Number of players tackled plus number of interceptions
- Clr : Clearances
- Err : Mistakes leading to an opponent's shot
- Touches : Number of times a player touched the ball. Note: Receiving a pass, then dribbling, then sending a pass counts as one touch
- TouDefPen : Touches in defensive penalty area
- TouDef3rd : Touches in defensive 1/3
- TouMid3rd : Touches in middle 1/3
- TouAtt3rd : Touches in attacking 1/3
- TouAttPen : Touches in attacking penalty area
- TouLive : Live-ball touches. Does not include corner kicks, free kicks, throw-ins, kick-offs, goal kicks or penalty kicks.
- ToAtt : Number of attempts to take on defenders while dribbling
- ToSuc : Number of defenders taken on successfully, by dribbling past them
- ToSuc% : Percentage of take-ons Completed Successfully
- ToTkl : Number of times tackled by a defender during a take-on attempt
- ToTkl% : Percentage of time tackled by a defender during a take-on attempt
- Carries : Number of times the player controlled the ball with their feet
- CarTotDist : Total distance, in yards, a player moved the ball while controlling it with their feet, in any direction
- CarPrgDist : Total distance, in yards, a player moved the ball while controlling it with their feet towards the opponent's goal
- CarProg : Carries that move the ball towards the opponent's goal at least 5 yards, or any carry into the penalty area
- Car3rd : Carries that enter the 1/3 of the pitch closest to the goal
- CPA : Carries into the 18-yard box
- CarMis : Number of times a player failed when attempting to gain control of a ball
- CarDis : Number of times a player loses control of the ball after being tackled by an opposing player
- Rec : Number of times a player successfully received a pass
- RecProg : Completed passes that move the ball towards the opponent's goal at least 10 yards from its furthest point in the last six passes, or any completed pass into the penalty area
- CrdY : Yellow cards
- CrdR : Red cards
- 2CrdY : Second yellow card
- Fls : Fouls committed
- Fld : Fouls drawn
- Off : Offsides
- Crs : Crosses
- TklW : Tackles in which the tackler's team won possession of the ball
- PKwon : Penalty kicks won
- PKcon : Penalty kicks conceded
- OG : Own goals
- Recov : Number of loose balls recovered
- AerWon : Aerials won
- AerLost : Aerials lost
- AerWon% : Percentage of aerials won
