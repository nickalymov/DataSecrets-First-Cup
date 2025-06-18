# DataSecrets-First-Cup
Machine learning solution for predicting the likelihood of a customer using a promo code. 7th place out of 76 participants in the competition. Link:[Leaderboard](https://datasecrets.ru/hackathons/7?aspect=leaderboard)

## Brief description
This project is designed to predict the likelihood of using promo codes by customers of the Dodo Pizza pizzeria service. The project uses data on orders, promotions, user activity and other features to train machine learning models based on gradient boosting and make predictions from stacking models.

## Project structure
- DataSecrets-First-Cup/
- │
- ├── my_data/                         # Data for training and testing
- │   ├── my_test.csv                  # Test data with added features
- │   ├── my_train.csv                 # Training data with added features
- ├── notebooks/                       # Jupyter Notebooks for Data Analysis and Development
- │   ├── EDA.ipynb                    # Exploratory Data Analysis Notebook data
- │   ├── feature_engineering.ipynb    # Notebook for generating new features from data
- │   ├── inference.ipynb              # Notebook for predicting test marks
- ├── submit/                          # Folder for storing results
- │   ├── submit.csv                   # Prediction results for test data
- ├── LICENSE                          # License
- ├── README.md                        # Project Description (this file)
- └── requirements.txt                 # Project dependencies

## Resume

### The Importance of Feature Creation and Modification
The key to this competition was the creation and modification of features for the training and test sets. I developed 56 new features that were added to the original data, which significantly improved the quality of predictions.

### Methods and models used
The strategy of stacking models and averaging their results was used for prediction. The following models were used:

- XGBClassifier
- LGBMClassifier
- CatBoostClassifier
  
### Training and validation process
The data directory can be downloaded from the official DataSecrets website at the link (registration required): https://datasecrets.ru/hackathons/7
The training set was divided into two stratified subsamples for validation. All three models were used on each subsample, and their results were averaged. The final label prediction was calculated as the average of all models on each subsample, which ensured more stable results. The general averaging formula was as follows:
(∑results of all models)/(𝑛=3×number of subsamples).

The selection of parameters for each model was carried out using the optuna library.

### Ideas that didn't live up to expectations
- Using pseudo-labeling:
Tried to improve the results by adding test data with labels obtained by the model to the training, taking into account the balance of labels (e.g. 1:33, where for every one used promo code there are 33 unused ones). However, this did not lead to a significant improvement.

- Stacking in pairs or using single models:
Experimented with different stacking combinations, including pairwise stacking of models and using single models (XGB, LGBM, CatBoost). However, these methods did not yield better results than the original stacking of all three models and averaging them.


Thus, the best results were achieved by working with features and a combined approach using several models, supported by hyperparameter optimization.

## License
This project is licensed under the MIT license. See the LICENSE file for details.
