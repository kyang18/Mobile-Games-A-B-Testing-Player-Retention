# Mobile-Games-A-B-Testing-Player-Retention
# Table of Contents
1. Project Background
2. About the Data
3. Analyzing Player Behavior
4. Comparing 1-day Retention
5. Comparing 7-day Retention
6. Conclusion

# Part 1: Project Background 
Cookie Cats is a hugely popular mobile puzzle game developed by Tactile Entertainment. It's a classic "connect three"-style puzzle game where the player must connect tiles of the same color to clear the board and win the level. It also features singing cats.  

As players progress through the levels of the game, they will occasionally encounter gates that force them to wait a non-trivial amount of time or make an in-app purchase to progress. In addition to driving in-app purchases, these gates serve the important purpose of giving players an enforced break from playing the game, hopefully resulting in that the player's enjoyment of the game being increased and prolonged.

But where should the gates be placed? Initially the first gate was placed at level 30. In this project, we're going to analyze an AB-test where we moved the first gate in Cookie Cats from level 30 to level 40. In particular, we will look at the impact on player retention.

# Part 2: About the Data
The data is from 90,189 players that installed the game while the AB-test was running. The variables are:

- userid - a unique number that identifies each player.
- version - whether the player was put in the control group (gate_30 - a gate at level 30) or the test group (gate_40 - a gate at level 40).
- sum_gamerounds - the number of game rounds played by the player during the first week after install
- retention_1 - did the player come back and play 1 day after SEE THE GATE?
- retention_7 - did the player come back and play 7 days after SEE THE GATE?
  
When a player installed the game, he or she was randomly assigned to either gate_30 or gate_40.

# Part 3. Analyzing Player Behavior 
50% of players played fewer than 16 game rounds during the first week after installation, and 75% of players played fewer than 51 rounds.

1. Nearly 4000 players did not even play a single round after installation. Possible reasons may include:
- They downloaded a number of new games at the same time and were attracted by other games.
- They opened the app but did not like the design/interface/music, so they quit even before playing the game.
- They have not started playing the game yet.

2. Another number worth attention is that more than 14,000 players played fewer than three rounds. For these players, the reasons for leaving may include:
- They did not enjoy the game. (This is probably the most common reason).
- The game turned out to be different from what they expected.
- The game was too easy and they got bored of it.

It is important to understand why a large number of players quit the game at an early stage. Tactile Entertainment can try to collect player feedback, for example, through an in-app survey.

# Part 4. Comparing 1-day Retention 
In the plot above we can see that some players install the game but then never play it, some players just play a couple of game rounds in their first week, and some get really hooked! What we want is for players to like the game and to get hooked.

A common metric in the video gaming industry for how fun and engaging a game is 1-day retention: the percentage of players that comes back and plays the game one day after they have installed it. The higher 1-day retention is, the easier it is to retain players and build a large player base.

Retention on Day 1: 44.52%
A little less than half of the players come back one day after installing the game. Now that we have a benchmark, let's look at how 1-day retention differs between the two AB-groups.

It appears that there was a slight decrease in 1-day retention when the gate was moved to level 40 (44.2%) compared to the control when it was at level 30 (44.8%). It's a small change, but even small changes in retention can have a large impact. But while we are certain of the difference in the data, how certain should we be that a gate at level 40 will be worse in the future?

There are a couple of ways we can get at the certainty of these retention numbers. Here we will use bootstrapping: We will repeatedly re-sample our dataset (with replacement) and calculate 1-day retention for those samples. The variation in 1-day retention will give us an indication of how uncertain the retention numbers are.

# Bootstrapping: Should we be confident in the difference?
<img width="484" alt="image" src="https://github.com/kyang18/Mobile-Games-A-B-Testing-Player-Retention/assets/76982420/41e9ffef-a679-497a-9c6d-a2058d7ac668">

These two distributions above represent the bootstrap uncertainty over what the underlying 1-day retention could be for the two AB-groups. Just eyeballing this plot, we can see that there seems to be some evidence of a difference, albeit small. Let's zoom in on the difference in 1-day retention

<img width="549" alt="image" src="https://github.com/kyang18/Mobile-Games-A-B-Testing-Player-Retention/assets/76982420/712c8d36-b6b9-40db-97d0-e8b6e52a4ab0">

From this chart, we can see that the most likely % difference is around 1% - 2%, and that 96% of the distribution is above 0%, in favor of a gate at level 30.

# Part 5. Comparing 7-day Retention
The bootstrap analysis tells us that there is a high probability that 1-day retention is better when the gate is at level 30. However, since players have only been playing the game for one day, it is likely that most players haven't reached level 30 yet. That is, many players won't have been affected by the gate, even if it's as early as level 30.

But after having played for a week, more players should have reached level 40, and therefore it makes sense to also look at 7-day retention.


version
gate_30    0.190183
gate_40    0.182000

Insights:

Like with 1-day retention, 7-day retention is slightly lower when the gate is at level 40 (18.2%) than when the gate is at level 30 (19.0%).
This difference is also larger than for 1-day retention, presumably because more players have had time to hit the first gate.
The overall 7-day retention is lower than the overall 1-day retention; fewer people play a game a week after installing than a day after installing.
But as before, let's use bootstrap analysis to figure out how certain we should be of the difference between the AB-groups.

<img width="516" alt="image" src="https://github.com/kyang18/Mobile-Games-A-B-Testing-Player-Retention/assets/76982420/885e11ba-ad42-4e43-ae39-4b87ac745767">

# Part 6. Conclusion
The bootstrap result tells us that there is strong evidence that 7-day retention is higher when the gate is at level 30 than when it is at level 40. The conclusion is: If we want to keep retention high — both 1-day and 7-day retention — we should not move the gate from level 30 to level 40.

There are, of course, other metrics we could look at, like the number of game rounds played or how much in-game purchases are made by the two AB-groups. But retention is one of the most important metrics. If we don't retain our player base, it doesn't matter how much money they spend in-game.

So, why is retention higher when the gate is positioned earlier? One could expect the opposite: The later the obstacle, the longer people are going to engage with the game. But this is not what the data tells us. The theory of hedonic adaptation can give one explanation for this.

In short, hedonic adaptation is the tendency for people to get less and less enjoyment out of a fun activity over time if that activity is undertaken continuously. By forcing players to take a break when they reach a gate, their enjoyment of the game is prolonged. But when the gate is moved to level 40, fewer players make it far enough, and they are more likely to quit the game because they simply got bored of it.

# I also use two methods to (Z-test & Z-test in Statsmodels) to do AB test.
The results of  A/B test indicate that the placement of the gate at level 30 is significantly associated with higher retention rates both after 1 day and after 7 days when compared to a gate placed at level 40. 

This suggests that players are more likely to continue engaging with the game when the first significant progress barrier they encounter is at the earlier level of 30 rather than at level 40.



