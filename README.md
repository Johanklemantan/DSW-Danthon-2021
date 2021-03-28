# DSW-Danthon-2021
## Make sure to download the dataset here before running my code. The dataset is too big to be uploaded here.
This model is able to predict with f1 score of 65,21 % and ranked top 32% of the total contestants.

### This dataset consist of 4 files.
- Train (70k++ rows)
- Irregularities (350k++rows) --> after deduplication become (190k++ rows)
- Alerts (7m++rows) --> after deduplication become (80k++rows)
- Test

### First Step :
__Irregularities consist of information such as speed gap, time gap between jammed and normal condition, jam level, etc__

1. Join train and Irregularities on s2 location
2. See the correlation between features and the labels
3. List some importance features and delete unimportant features

### Second Step :
__Alerts consist of information such as weather, accident, street type, etc__
1. Join train and Alerts on s2 location
2. See the correlation between features and the labels
3. List some importance features and delete unimportant features

### Third Step :
1. Join Alerts and Irregularities based on 'supergabungan' which is combination of s2location, time, and hour
2. See that we know important features in each table, we can make new features and delete unimportant features
New features generated based on __my__ observations are :
- Road Type (Whether the road is main street or not)
- Condition Type (Accident, Bad Weather, etc)
- Relialibility
- Rating Rate
- Jam Trend
- Jam Level
- Alerts Count
3. Let's say the new dataset from alerts and irregularities calles 'combination'

We also construct new features such as __isweekend__ and __isbusyhour__ from the date and time

### Fourth Step :
1. Join train and combination on day_hour by taking the day and hour from s2idtoken

### Cleaning the Data :
There are several way to clean the data.
Here's some method that I've tried :
- fillna with bfil, ffil, pad, backfill
- Impute with mode
- Try to fill the nan value by search the similarity each location (very tryhard)
But after all, the best score by training is using fillna ffil.

We are using 5 models to compare, which are :
1. Random Forest Classifier
2. XG Boost Classifier
3. Logistic Regression
4. Decison Tree Classifier
5. Naive Bayes

F1 Score Before Tuning :

#### Hence, we tried to do hyperparameter tuning on Random Forest, Decision Tree, and Naive Bayes

F1 Score after tuning result :
1. Random Forest Tuned : 0.757 (increased 0.0002 XD)
2. Decision Tree : 0.756 (increased 0.001)
3. Naive Bayes : 0.797 (increased 0.01)

### Fifth Step :
1. Join test and combination on day_hour
2. Find the prediction by fit the model
3. Make sure the format is same with sample_submission
4. Post in Kaggle and try your luck !


For you who wants to try this problem, you can get the dataset here : 
<a href:'https://www.kaggle.com/c/danthon2021/data'>Kaggle</a>

Thankyou for reading !
Happy Coding

