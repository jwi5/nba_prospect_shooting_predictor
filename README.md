# NBA Prospect Three-Point Shooting Predictor
![Image Alt text](/Images/buddy.webp)
## Business Understanding
### The Evolution of the NBA and the Rise of Three-Point Shooting
In the modern NBA, the [emphasis on three-point shooting has dramatically reshaped the game](https://www.nba.com/news/3-point-era-nba-75), altering team strategies and player development. This evolution has [elevated the importance of proficiency in three-point shooting](https://www.theringer.com/nba/2021/2/12/22279459/nba-make-miss-3-point-shooting) to an essential skill for players across all positions. Being adept at long-range shooting is now a critical factor in a player's career, influencing their ability to secure a spot on a team and potentially impacting their market value. As a result, NBA teams are [increasingly focusing on developing this skill in their players](https://www.cbssports.com/nba/news/thunder-hire-chip-engelland-nbas-top-shooting-coach-who-spent-17-years-with-spurs-per-report/), leveraging targeted training and analytics to enhance shooting effectiveness.
### Challenges in Evaluating Three-Point Shooting Talent
As the NBA's emphasis on three-point shooting continues to grow, its impact on the draft and scouting processes has become increasingly significant. However, [accurately projecting a college player's three-point shooting ability to the NBA level is a challenging aspect of scouting](https://theboxandone.substack.com/p/can-we-trust-pre-draft-shooting-improvements#:~:text=Shooting%20is%20such%20an%20important,the%20ultimate%20mental%20torture%20chamber.). This difficulty arises because players' shooting performances can vary widely once they transition from college basketball to the professional stage. Some players may significantly improve their shooting due to advanced training methods and a focus on skill development, while others may struggle to replicate their college success or fail to develop their shooting abilities further.

[A key issue in this scouting dilemma is the relatively small sample size of three-point shooting attempts in college](https://fansided.com/2020/07/20/nba-draft-shooting-synopsis-volume-versatility/), which can lead to unstable and misleading percentages. This makes it hard for scouts and teams to confidently predict which players will continue to excel as three-point shooters, who will improve with time and training, and who might not transition their shooting skills effectively to the professional level. Despite the critical role of three-point shooting in determining a player's impact in the NBA, the unpredictability of shooting development post-college remains a significant challenge for teams looking to draft prospects with the potential to excel in today's game.
### Predictive Modeling: A Solution to Three-Point Shooting Evaluation
Given the challenging and often unpredictable nature of assessing college prospects' three-point shooting capabilities for the NBA, this project aims to leverage predictive modeling and machine learning techniques to forecast a player's three-point shooting performance at the professional level. By utilizing a comprehensive dataset of college statistics from current NBA players, with their NBA three-point shooting percentages serving as the target variable, this approach seeks to identify patterns and predictors that may not be immediately apparent through traditional scouting methods.

The rationale behind employing predictive modeling lies in the inherent randomness and difficulty associated with evaluating three-point shooting potential. NBA front offices could greatly benefit from a methodology that offers a more accurate prediction of a prospect's ability to shoot from long range, based solely on statistical analysis. This would allow teams to allocate their scouting resources and attention more efficiently, focusing on assessing other aspects of a player's game that are less random and more observable through traditional evaluation methods.
This strategic shift in talent evaluation emphasizes the development and recognition of well-rounded players, while still acknowledging the critical role that three-point shooting plays in the modern NBA. Through this project, I aim to provide NBA front offices with a tool that enhances their ability to predict three-point shooting success, optimizing the draft and development process by using data-driven insights to complement traditional scouting expertise.
## Data Understanding
In this project, I aim to predict the NBA three-point shooting percentages of college basketball prospects. To achieve this, I have sourced and combined comprehensive datasets that encompass both NCAA player statistics and NBA player three-point shooting statistics. Understanding the structure, content, and quality of this data is crucial for my analysis and subsequent predictive modeling.
### NCAA Player Statistics
The dataset for [NCAA player statistics was downloaded from BartTorvik.com](https://barttorvik.com/playerstat.php?link=y&year=2024&start=20231101&end=20240501), covering every NCAA season from 2007-08 to 2021-22. This dataset includes a wide range of player statistics, such as points per game, assists, rebounds, and, critically for my project, three-point shooting percentages. After downloading the CSV files for each season, they were merged into a single CSV file to create a comprehensive dataset. This consolidation process was essential for analyzing trends over time and ensuring a robust sample size for our predictive models. Importing this combined dataset into a Pandas DataFrame allows for efficient data manipulation and analysis within a Python environment.
### NBA Player Three-Point Shooting Statistics
For the NBA player statistics, I focused on three-point shooting data from the regular seasons spanning from 2008-09 through the current season, as I only had access to college player data beginning in the 2007-08 season. This data was [sourced from Stathead.com](https://stathead.com/basketball/player-season-finder.cgi), specifically selecting players with a minimum of 82 games played to ensure I am considering only those with a significant amount of playtime, thereby improving the reliability of the three-point percentage as a metric. This dataset provides a critical linkage to the NCAA dataset, as it enables us to compare college performance with professional outcomes, focusing on the aspect of three-point shooting. Most of the statistics in this data set will be Per 100 possessions, as we will need this to update the target variable, as I will explain in detail in the Data Cleaning section.
### Caveats and Considerations
An important caveat of this project is the exclusion of international prospects and players from the G-League Ignite who are increasingly making up a significant portion of NBA draft picks each season. This exclusion is due to the unavailability of comparable and consistent data for these groups that align with the NCAA dataset. This limitation means the predictive model may not fully capture the broader spectrum of talent entering the NBA, as the pathways for developing basketball players continue to diversify beyond traditional college basketball.
## Data Cleaning
### Target Engineering
When assessing NBA three-point shooting skill, it's crucial to recognize that not all three-point shots are created equal. A simple three-point shooting percentage, while useful, doesn't fully capture a player's shooting ability. This metric can be misleading, as it doesn't account for the context in which shots are taken. Players who only attempt three-pointers when wide open may have inflated percentages compared to those who frequently shoot under more challenging conditions.

To address this discrepancy and create a more nuanced target variable for our predictive modeling, I have refined the traditional three-point shooting percentage. Our engineered target metric adjusts a player's three-point percentage by considering the volume of three-pointers attempted per 100 possessions. This adjustment acknowledges that players who shoot more often are likely taking harder shots, thus providing a better indicator of true shooting skill.

Additionally, we've introduced a slight adjustment factor based on the total number of three-point attempts a player has made over their career. This factor is rooted in the principle that a larger sample size of shot attempts offers a more stable and reliable measure of a player's three-point shooting talent. It accounts for the variability and noise in shooting percentages, especially in cases where players have fewer attempts. Essentially, our engineered target variable aims to balance percentage accuracy with shot difficulty and confidence in a player's shooting ability derived from their attempt volume.

This methodological refinement ensures that our predictive model considers not just how accurately players shoot from beyond the arc, but also the context of their shooting—leading to a more accurate assessment of three-point shooting skill in the NBA.

After creating the Confidence and Volume-Adjusted 3P% metric, here is how our list of top 20 shooters by percentage changed:
![Image Alt text](/Images/threep_comp.png) ![Image Alt text](/Images/threep_comp2.png)

Drawing on domain knowledge, the Adjusted 3P% metric emerges as a superior indicator of three-point shooting prowess. For instance, Stephen Curry, widely acknowledged as the greatest three-point shooter in history, ascends from 8th place based on traditional 3P% to the top position when considering Adjusted 3P%. Conversely, Tony Bradley, who leads in three-point percentage, experiences a significant drop in the rankings due to his low rate of 0.3 three-point attempts per 100 possessions. Bradley, primarily a center who rarely shoots from beyond the arc, has only attempted 12 three-pointers in his career, suggesting that his 50% success rate is more likely a result of small sample variance rather than genuine shooting prowess. Another notable example is Kelenna Azubuike, recognized as a proficient three-point shooter but not among the elite. While he ranks fourth in traditional 3P%, his position drops out of the Top 20 in Adjusted 3P% due to taking only 4.5 three-point shots per 100 possessions throughout his career. This adjustment reflects a more nuanced understanding of a player's ability to shoot three-pointers, accounting for both accuracy and the difficulty level of the shots attempted.

### Cleaning the NCAA Data
The process of cleaning the NCAA player dataset started with the elimination of entries for college athletes sharing names with NBA players, or NBA players who were in college before the 2007-08 season (the first season I have college data), but share a name with player(s) in college after between the 2007-08 and 2021-22 season. This ensured a distinct set of individuals for analysis. This initial step resulted in a curated list of 559 unique players.

Subsequent efforts focused on consolidating the data for athletes with multiple seasons of college play. This was achieved by aggregating individual season statistics into a single row per player. To further refine the dataset, statistical percentages from each player's final college season were assigned increased significance compared to earlier seasons. This approach was predicated on the rationale that a player's most recent performance is likely a more accurate indicator of their current abilities and potential future success.

## Modeling
Several regression models were used: Linear Regression, Ridge Regression, Random Forest Regression, Support Vector Regression, XGBoost Regression, and AdaBoost Regression. The effectiveness of each model was assessed based on the R-Squared and Root Mean Square Error (RMSE) on Cross Validation.
![Image Alt text](/Images/model_performance.png) 

Based on these cross validation results, I chose the Support Vector Regressor as the best model and used it to predict on the test set:

SVR Performance on Test Set:

R-squared: 0.4879032797541556

RMSE: 0.06343820309154603

The RMSE shows that, on average, the model's predictions of the NBA three-point shooting percentage (3PT%) deviate from the actual values by 6.34%. Although this accuracy might not appear exceptional at first glance, it surpasses the predictions made by our baseline Dummy Model by a notable margin of 2.71%. This improvement is particularly significant given the acknowledged difficulty in accurately predicting NBA three-point success from an NBA prospect's profile. 

## Feature Importance
Feature Importance in the SVR Model was assessed through Coefficent Magnitude and Perumtation Feature performance. Here are the results:
![Image Alt text](/Images/coefficent_magnitude.png) 
![Image Alt text](/Images/permutation_importance.png) 

## Conclusions
When assessing the coefficient magnitude and the permutation feature importance, FT% (free throw percentage), 3PT/100 (Three-Pointers per 100 Possessions), 3P (three pointers made) are consistently important predictors of NBA three-point shooting skill. This aligns with the previous discussion of three-point percentage alone not being as indiciative of three-point shooting skill as it might seem, as some players may be taking a higher volume of shots per possession and also may be taking more difficult shots as a byproduct of this. Additonally, players generally dont take that large a sample of three pointers during their college careers, so college three-point percentage is quite susceptible to noise, making it less reliable for predicting future performance.

Free throw percentage (FT%), on the other hand, can be a better predictor for a few reasons. First, it shows how well a player can shoot when conditions are controlled - no defenders, same distance every time. So is also arguably as good at, if not better at, indiciating a player's overall 'shooting touch' than three-point percentage. Another factor is players usually take many more free throws in college than three pointers, and free throws are less prone to variance in general because they are higher-percentage shots, so this gives us a larger sample to work with and is a more reliable measure of a player’s shooting ability.

The stat 3PT/100 is also useful. It tells us not just how many threes a player makes, but how willing they are to take them. Good shooters are likely to shoot more threes, both because they themselves have been considered good shooters in the past (high school and team practices) and because their coaches set up plays for them to shoot from distance. Also, if a player is shooting more threes per possession, they’re probably taking more difficult shots too, rather than only shooting when they find themselves wide open. And it is also possibly true that shooting more often in games might indicate and/or lead to better shooting improvement and developement in the future.

Overall, these findings show that how often players shoot and their free throw percentages might give us better clues about their future NBA three-point shooting than just their college three-point shooting percentage. This approach recognizes that predicting shooting skill is about more than just the percentage of three pointers a player makes; it's also about their overall shooting habits and how they fit into the game.

## Repo Structure 
```
├── Data
├── Images
├── Notebooks
├── .gitignore
├── Final.ipynb
├── LICENSE
├── README.md
```

