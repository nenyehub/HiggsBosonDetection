# HiggsBosonDetection
Identifying the Higgs Boson particle with Machine Learning! Model selection, hyperparameter optimization, and model performance metrics.

## Model Selection and Hyperparameter Optimization
In this notebook, I perform hyperparameter optimization on two models with the help of kFold cross validation. I do this with the help of kFold cross validation and AUROC score. Instead of performing standard kFold validation to validate a model's performance (k-1 sets for training and the 1 held out set for validation) I do the following: 

1) Import *training* data only

2) Split training data **further** into training and validation sets. This validation set will remain *untouched* for now

3) Split the training set **further** into k subsets with 1 held-out validation set (kFolds)

4) On each iteration of the kFolds technique: 
    - k-1 sets are used for training the model with hyperparameter(n)
    - 1 held-out set is used to calculate the AUROC score of the model with hyperparameter(n) 
    - Change the value of n
    
5) Choose the hyperparameter value that resulted in the highest AUROC score

6) Evaluate the model with optimized hyperparameters on the *untouched* validation set 

And so, rather than using kFold cross-validation to validate the accuracy of a single model across k subsets, I am using each subset to test the model with **different** hyperparameters. I then select the hyperparameter value which produced the highest AUROC score and retrain the model using this value. Afterwards, I validated the model's performance on the *untouched* validation set from the first split I performed on the training data (step 2). 

What this approach does:
* Prevents model overfitting by *first* performing hyperparameter optimization *then* validating the model on an untouched set 
* Model validation performed on the untouched validation set 

What this approach **does not** do: 
* Actual kFold cross validation

## Model Validation
And so, although the above steps may be misleading because I use the kFolds technique, I do not use kFold splitting to *validate* my model, but rather to test and select the optimal hyperparameter. I then perform a simple one-step validation using the set I split off in step 2.

## Model Selection and Performance Metrics
I performed the above hyperparameter optimization and validation strategies on two learning algorithms: kNearestNeighbors and Decision Trees. The metric I used to evaluate each model's performance is their AUROC scores as derived in step 6. I compared both scores and chose the model with the higher AUROC score. 

To summarize my results, I found k = 23 to be the optimal k-value for kNN, and max_depth = 7 to be optimal for my decision tree. Thinking about this now, if I wanted to optimize the models further I could repeat the same process with other hyperparameters to try to improve performance. However, I think I chose the most impactful hyperparameters to adjust because of the large variance in AUROC scores throughout my iterative testing process. 

## Result of Analysis 
The winning model turned out to be my Decision Tree, by a large gap: AUROC score of .73 compared to .63 with kNN. This is clearly visually represented by the graphed ROC curves that show the large difference in area under the curve between the two models. 

This analysis has shown me why it's so important to 1) Pick the most effective model, 2) Optimize it's hyperparameters, and 3) Evaluate its performance on a validation set. These three steps maximize your model's effectiveness, prevent overfitting, and make sure you pick the best model for the situation. I will definitely be using these techniques to compare model performance in the future. 

*Notes:*
- Because of randomized data splits, running the notebook gives slightly different values for the best hyperparameters each time. My code automatically uses the 'best' value to create the final model, and so the models' performance may vary slightly each time the notebook is ran. 
- Originally I was performing between 10 and 15 splits with the kFold technique, and evaluating 10-15 different hyperparameters. After the completion of this notebook, while writing this top portion, I had the idea that since this is such a large dataset, I could do something super large such as 100 splits. Testing 100 different hyperparameters might actually give me more optimal values than testing with 10-15, so I tried this out. Very interestingly, even testing 100 different k-values with kNN resulted in an optimal k very close to the one I found testing only 15. The same exact thing can be said about the decision tree.

*by Chinenye Ndili*
