Welcome to my FIFA Moneyball Project

Objective:
This is my first python project in Ironhack. It consists of a python data analysis exercise in which I develop a Linear Regression Model to infer each player's market value and a bonus part in which I extract some interesting insights from the dataset. 

Data:
The data comes from the following website: https://sofifa.com. It contains information regarding a large amount of football players. This information ranges from each player's skills to his contract's information.

Steps covered:
1. Downloading packages

2. Importing packages

3. Loading data

4. Cleaning data:

In this part, I focus on three aspects:
- Improving the readibility of the columns
- Selecting the information which is going to be useful for our objectives
- Cleaning values so we can work with them

4.1. Standardize headers: this helps me deal with column names more easily as they have the same format across the df.

4.2. Dropping irrelevant columns:
I drop the 'id', 'name', 'player_photo' and 'flag_photo' as it does not add any valuable information for the purpose of this exercise. 
I drop 'bov' because it is redundant information already covered in 'ova'

4.3. Cleaning weight and height data and transforming to metric units

In this part I change the format of the data to metric units (being from spain, this makes the data easier to understand) and to integers, so we can treat them as numerical data from now onwards.

4.4 Dealing with 'position':
'bp' stands for best position, which is the information we find relevant as a player's value will be more influenced by its best position rather than by all his potential positions.

Therefore, we drop 'position' data and we will use 'bp' so as to know each player's position.

Moreover, position has more NaN values than bp.

4.5. Dealing with columns which show a player's score in all positions:
The 'ova' of each player has the same score as the players' score in his best position.
Therefore, we can drop columns which show each player's score across all positions as long as we keep their 'ova' and 'bp'.
This way we are reducing the redundancy of our data and simplifying the dataset. Less is more.

4.6. Getting each player's contract information:
We drop team_&_contract as we have the same data in two other separated columns: 'team', 'contract'. We apply a function to the 'contract' column to extract each player's contract duration.

We also need to clean all the columns that contain info regarding sums of money: 'release_clause', 'value', 'wage'. We do so using a function we have defined.

4.7. Dealing with null values:

I first see which columns have null values and how many are they in each column. 

Many columns have 58 NaN values, which are the same rows for each case. Removing them from one column solves it.

Additionally, we delete composure NaN values as they are not significally relevant. For time constraints we do not replace them by its mean.

We need to deal with the column with the most NaN values: 'loan_date_end'. We create another column that stores the relevant information from that column: wether the player has been loaned or not. This new column is named: 'loaned?'

4.8. No comments needed.

4.9. Analysing categoricals:
I drop 'nationality' and 'club' because they contain really fragmented values. There are no 5-10 values covering around 80% of the data.

I also group the 'bp' values in 4 categories: defenser, midfielder, forward and goalkeeper so as to keep the minimal information necessary that will be useful for the model. The assumption here is that by knowing if a player is within one of this 4 categories we already get the valuable information this column can facilitate us.

---

From this point onwards it is important to understand what the workflow of the project was.

First I thought that splitting the df in Goalkeepers and players would result in a more accurate Linear Regression Model as some columns were only useful for infering Goalkeeper's value and viceversa. After trying to do so, I found out that the assumption was wrong (at least for the level of sophistication that my approach had).

In the steps 6,7 and 8 I carry the steps that follow the mentioned assumptions. In step 9 I dismiss that thought process and create a Linear Regression Model using the df without differentiating between types of players.

After removing numerical outliers, normalizing them and encoding categoricals, I get a model with a 0.93 R2. Pretty good considering that my first model had an R2 of 0.23. 

---

Questions:

1. Does the release_clause of a player and its value have any correlation?¶

There is a correlation between these two factors. Nevertheless, it is interesting to see that this correlation is not linear since when the release_clause is 0, the value of the player is not 0.


2. How does stamina and height affect the sprint_speed of a player?

We can see that there is a positive correlation between stamina and sprint_speed. Additionally, we can see thanks to our colour gradient that slow players have lower stamina and are higher. The opposite happens for fast players.

# Failed question:
In this case I wanted to show the average value for each age and the distribution of bp across each age.
I haven't been able to find a way to show the average value though.