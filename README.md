# Higgs Boson Particle Detection

## 1) Model comparison
I compared four classifiers: kNN, Decision Trees, Random Forests, and Gradient Boosted trees. I beleive the Gradient Boosted trees works the best, so I used an ensemble of those classifiers in my final model. I used the area under each model's ROC curve to determine this. The higher the area, the better I perceive the model to be. The Gradient Boosted trees resulted in the highest AUROC value, and so I used this model as the estimator in the final ensemble.

## 2) Data used for training
I used 70% of the data in train.csv for training, and the other 30% for validation. In the hyperparameter testing phase, I split the 70% into k subsections, to train models with different hyperparameters. For the final model I submitted to Kaggle, I used an ensemble of Gradient Boosted trees and trained it on the entire 70% training data rather than the k-split subsection. 

## 3) Hyperparameter Selection
I chose the hyperparameters by systematically running through many different values and choosing the hyperparameter value that resulted in the highest AUROC value (evaluated on a kFold split of the training dataset). 
