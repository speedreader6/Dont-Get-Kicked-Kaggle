# Dont-Get-Kicked-Kaggle
Random Forest approach to a classification problem with limited time.

###Overall Approach
I examined the counts and plots of data variables and noticed that many of the categorical features contained hundreds of levels. A quick experiment showed that creating dummy variables for all of these levels would run my PC out of memory. Thus, I chose to apply a random forest classifier since its sklearn implementation is supposed to handle categorical variables more or less out of the box with no need for dummy variables. 

###Data Transformation
I merged train and test data to perform the transformations simultaneously. Dates were converted to days since the start of 2009. All missing values of numeric variables were filled with the median and categorical variables - with another level. In case of cat. Variables that were detected as numeric by the code, the first approach is equivalent to the second. All categorical variables levels were converted to numbers. Numeric variables were scaled to 0-1 range. Finally train and test data was separated.

###Validation
I split the training data into 10 roughly equal groups for a 10-fold cross-validation approach, i.e. each give sample was used as a training set against a model trained on the remainder. RefId and pre-processing identifier columns were excluded from analysis. Recall and Precision were recorded for each fold. Mean recall was 0.79, and mean precision was 0.24. Mean F1 score for bad cars (the harmonic mean of the recall and precision) was 0.36, which is adequate.Final model was trained on the entire training set. Its performance in terms of these metrics on the test set is unknown since I was not able to find the results on Kaggle.

###Potential Improvements
Unfortunately the methodology used is motivated by time and resource constraints. Ideally I would compare other approaches such as SVM, logistic regression or gradient boosted trees, not to mention searching the literature for most recent methods of dealing with dense categorical variables. This latter problem could also be addressed by variable selection. All of these models can be part of an ensemble model with weights proportional to their performance metrics in cross-validation.

The current solution rests on random forests’ ability to control overfitting on their own, but this problem could be attacked directly with tools like PCA. A more sophisticated approach could use NLP to bin car models together and creating so-called direct zip code models. The latter is essentially a sub-model that uses external demographic data by zip code along with IsBadBuyRate to model this rate by zip code and bin the codes together into broader groups. I could have also used the variable importance output of random forest model for variable selection for a future model, although the current model results did not reveal particular insights along these lines. The complexity of working with dense variables and memory constraints they create limited my ability to address this issue.

Lastly, the unbalanced nature of the classes in the data could be addressed with bootstrapping.
