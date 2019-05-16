# Predicting NBA Player Salary


## Overview

This project took various NBA player data and used it to build a linear regression model. The model predicts the NBA player salary for the Free Agents following the 2017-18 Season.

Blog post on the topic can be found [here]("https://datatostories.com/posts/2019/04/19/nba-salary-predictions/").

## Project Design

I chose to predict player salaries in the NBA out of personal interest. I've always been interested in how salary dynamics in professional sports work and wanted to see if player statistics can help predict the salary for the next season. 

I chose to scrape data from various sports website (all listed in the Data Section). Upon cleaning the data, I had close to 2260 player statistics; I ran a linear regression model on 19 features that showed strong correlation with the target variable (Salary) and added features using polynomials (degree 2 terms and feature interaction terms). The best model produced was a linear regression model with ridge regularization applied. The alpha value for the ridge regularization was 8.21, the mean absolute error on the training set was \$3.04M, and the R^2 score of 0.5619. 

Some potential improvements can be made, and some that I want to implement include adding more player information, measuring his popularity on the web (Twitter, Instgram), and factoring NBA financial structures into the account. 

## Application

A model that performs well to predict NBA Salaries can be of many use:

- NBA Executives can use to determine if a player they are targeting is worth the contract he is asking for.
- Agents or players can set themselves an expectation about how much money they want to ask for during Free Agency
- Similar modeling can be done with other sports (i.e. Baseball, Soccer); in fact, data analytics in sports is more popular than ever and this could very well be in effect.



## Tools

- Web Scraping: Selenium
- Data Storage: Pandas, pickle
- Data Visualization: seaborn, matplotlib
- Data Analysis: Statsmodel, Scikit-learn
- Presentation: Google Slides

## Data

The data was obtained by scraping the following websites:

1. Basketball-Reference.com: Player stats by year from 2008-09 seasons to 2017-18 seasons, Rookie lists from 2008-09 seasons to 2017-18 seasons
2. HoopsHype.com: Player salaries from years 2009-10 to 2018-19 seasons
3. Spotrac.com: Free Agent lists from 2011 to 2018

The data were accumulated and then combined to create a single dataset of 2260 total observations. The features used were accumulated are listed in the Appendix.

## Appendix: Features Used

| Features | Type         |  Description | 
| -------- | ------------ |------------- |
| G  | Int |Number of Games the player played in the past 3 seasons |
| GS  | Int |Number of Games the player started in the past 3 seasons|
| MP  | Float |Minutes played per game in the past seasons |
| 2PA  | Float | 2 Points attempted in the past 3 seasons |
| FGA  | Float | Total field goals attempted in the past 3 seasons |
| FT  | Float | Total free throws made in the past 3 seasons |
| 3P  | Float | Total 3 points field goals made in the past 3 seasons |
| DRB  | Float |Total defensive rebounds grabbed in the past 3 seasons |
| ORB  | Float |Total offensive rebounds grabbed in the past 3 season|
| AST  | Float |Total assists in the past 3 season|
| BLK  | Float |Total blocks in the past 3 season |
| TOV | Float |Total turnovers in the past 3 season|
| PTS  | Float |Total points in the past 3 season|
| VORP  | Float |Total defensive rebounds grabbed in the past 3 season |
| USG%  | Float | Usage rate: how much a player possesses the ball on offense|
| STL%  | Float | A player's steal rate in a game |
| DBPM  | Float | Defensive Plus/Minus: measures a player's defensive contribution by looking at how much his team outscores (or is outscored by) the opponent |
| TOV%  | Float |A player's turnover rate in a game |
| DWS  | Float |Defensive Win Share: measure's a player's defensive contribution by looking at how many wins he is responsible for |