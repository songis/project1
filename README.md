Project 1
========

The project for the first half of the semester is due on October 24th as a pull
request to this repository. The emphasis for this projet is on data analysis
using tools of reproducible research including version tracking, knitr, and R
markdown. You are free to answer any question you want, but you must provide a
quantitative report that utilizes the material we have covered durign the first
half of the semester.

***Ground rules...***
* Your document should layout your question in the introduction, provide a brief
synopsis for why it is important, describe how you obtained the data, your general
approach to analyzing the data, a summary of your results, a discussion, and
mention of what your future directions would be.
* You should post your project as a pull request to this repository as `*.Rmd`,
`*.md`, and `.html` files. Prior to submitting the files, you should set
`echo=FALSE` for all of the code chunks. This will hide the R code in the final
document.
* The final document should be approximately 5 pages when the code chunks are
hidden and  you use a normal sized font.
* I don't care what your question is or what subject domain it covers. The key is
that it needs to be data driven. Microbiology, video game statisitics, immunology,
whatever. Do something where it will be easy for you to come up with an interesting
question and fun analysis.

---
title: "Project 1"
output: html_document
---

Introduction
  Background information on League of Legends
    General gameplay
    LCS
    Relevant statistics
  Is there a correlation between win rate and KDA ratio, gold per minute, minions killed, or champions killed?
  Importance: Determining the factors for victory in LoL
  Approach to data analysis
    LCS Summer 2014 data
    Spearman correlation(?) comparing win rate with each of the independent variables
Data
  Table with Summer 2014 LCS data
  Description of data and its origin
Results
Discussion
Future Directions
  Possible implications of results
  
**Introduction**
  
League of Legends, widely known simply as LoL, is a PC game categorized as a "MOBA," or "Multiplayer Online Battle Arena."  It is a game in which two teams of 5 players each face off to achieve the ultimate goal of destroying the opposing team's Nexus.  Each player controls a single "champion" who gets stronger as the game progresses, buying items with gold.  Gold is gained by killing "minions" that continuously push towards each enemy's nexus, taking down neutral monsters or enemy structures, and killing enemy champions.  All champions also receive a set amount of gold continuously throughout the game called "ambient gold."  Generally, a team with a gold lead has an advantage in fighting strength that becomes more significant as the gap in gold increases.  A sizable gold lead thus bestows a much higher chance of victory.  

To clarify some of the statistics tracked in LoL, there are 5 that will be studied in this analysis: win rate, KDA ratio, gold per minute, minions killed, and champions killed.  Win rate is self-explanatory.  KDA ratio refers to (K+A)/D, in which K is the number of kills, A is the number of assists, and D is the number of deaths.  Gold per minute is the average amount of gold earned per minute of a game, taking into account any sources (e.g., minion kills, champion kills, ambient gold, etc.).  Finally, minions and champions killed refer to how many kills were achieved against enemy minions and champions.  There is far more to the game that has not been explained, but for the purpose of understanding this report, the explanation is sufficient.

The rise in LoL's popularity as the most popular game in the world has been accompanied by the explosive growth of its professional scene.  In North America and Europe, it is called the League of Legends Championship Series (LCS), of which there is both an NA and EU variant.  A single season of LCS consists of 8 teams and 28 total games.  Each team plays every other team in its respective region 4 times and is ranked at the end of the split by its number of wins.  The data that I will be analyzing is based on the combined stats of NA and EU's 2014 summer split.

The question to be addressed is: Is there a correlation between win rate and KDA ratio, gold per minute, minions killed, or champions killed, in games of LoL at the professional level?  In reality, there are many different ways to find victory in LoL.  Depending on what champions are picked and how each team plays, these can vary from chaotic 5v5 team fights, picking off singled out opponents, outmaneuvering the enemy in taking down structures, and everything in between.  It is unclear as to whether there are any variables that are consistently correlated with win rate.  Revealing any variables that show such correlations could provide evidence for the most effective and ineffective strategies, which is a topic that has been debated in the game for years.  Professional players have always struggled to find the best strategies; whether any are objectively (or at least evidently) superior to the rest remains to be discovered.

I would like to begin this analysis of win rate correlation by studying the aforementioned variables: KDA ratio, gold per minute, minions killed, and champions killed.  First, I will draw a scatter plot to check the distribution.  If the data seems to follow a normal distribution, I will test for parametric Pearson correlation to determine correlation between each of the independent variables and win rate.  Otherwise, I will test for non-parametric Spearman correlation.  I hypothesize that each of these variables are positively correlated with win rate due to the fact that increasing any of these variables either grants or is indicative of a team's advantage in game.  I believe this advantage will more often than not be translated into victory.

**Data**

```{r}
LCS.table<-read.table("LCS Statistics (Summer 2014).txt",sep="|",header=TRUE,stringsAsFactor=FALSE)
LCS.table
```