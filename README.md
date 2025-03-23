Overview:
This project handles data preprocessing, missing data imputation, and model training using CatBoost with hyperparameter tuning. The process is divided into three main steps:

Data Preprocessing

Missing Data Imputation

CatBoost Model Training with Hyperparameter Tuning

1. Data Preprocessing

The dataset is loaded from a CSV file. Rows with missing values in the target column, "Prediction," are removed to ensure the data used for training is clean and complete.

Next, the columns "Magnetic Field Strength" and "Radiation Levels" are processed to extract numeric values from categorical data. For example, if a cell contains "Field-100," the number 100 is extracted and converted to a numeric format. This ensures the data is ready for numerical modeling.

After cleaning, the dataset is split into features (X) and the target (y). X contains all columns except "Prediction," which becomes the target variable.

2. Missing Data Imputation

The dataset may still have missing values. To handle this, imputation is done in two stages:

a) Decision Tree Imputation for Categorical Features

Missing values in "Magnetic Field Strength" and "Radiation Levels" are filled using Decision Tree models.

The trees are trained on rows where values are present, learning patterns from other features to predict the missing ones.

If a pre-trained model is available, it is loaded to avoid retraining on new data.

b) Grouped Median Imputation for Numerical Features

Remaining numeric columns are imputed using the median values grouped by "Magnetic Field Strength" and "Radiation Levels."

If a group has no data, the overall median for that column is used instead.

This approach preserves the relationship between numeric features and categorical ones.

After imputation, the trained models and median values are saved to a file for later use on new datasets.

3. CatBoost Model Training with Hyperparameter Tuning

The next step is to train a classification model using CatBoost. To improve performance, hyperparameters are tuned using a randomized search.

The search explores different combinations of:

Learning rate

Tree depth

Number of estimators

Subsampling ratios

Column sampling ratios

Bootstrap type (set to "Bernoulli" for compatibility)

The RandomizedSearchCV function runs multiple configurations and evaluates each using 5-fold cross-validation. This ensures the model generalizes well to unseen data.

Once complete, the best combination of hyperparameters is selected, and the corresponding model is saved.

Final Output:

By the end of the process:

The imputation models and medians are saved for future datasets.

The dataset is fully cleaned and imputed, ready for analysis or further modeling.

The best-performing CatBoost classifier is tuned and saved.
