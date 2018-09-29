# Ames, Iowa Housing Dataset

*Jon Nelson*

### Problem Statement

Is there an influence on the sale price of a home in Ames, Iowa based on the neighborhood in which you live?

### Description

Using a dataset about the homes in Ames, Iowa I explored all of the different housing features that are used to value a home in order to build a production level model to predict each homes sale price.

### Modeling

After cleaning the data, performing exploratory data analysis, and performing some feature engineering I have created a final features dataset to feed into my regression models.

Those models scored as follows:

| Model                   | Train Score | Test Score |
|-------------------------|-------------|------------|
| Linear Regression       |   0.9214    |   -1.3689  |
| GridSearch w/Ridge      |   0.8584    |    0.8799  |
| GridSearch w/Lasso      |   0.8157    |    0.8566  |
| GridSearch w/ElasticNet |   0.8248    |    0.8658  |

Using a pipeline I was able to setup a sequential process of steps to use when creating my models. With this pipeline I could then feed all of these steps into a GridSearch to search for the optimal parameters. These pipeline steps included:

- Variance Threshold
- SelectKBest
- [Model of Choice]

After running each of the above mentioned models through my pipeline and GridSearchCV I found the optimal model to be the GridSearch w/Ridge model based on the accuracy score. It was able to explain around 85.84 % of the variance in my model on my training data and 87.99 % of the variance in my model on my testing data.

#### GridSearch

GridSearchCV is a modeling technique that searches for the optimal hyper-parameters provided during the instantiating of the model. Using its built in cross validation it can search over the grid of the provided hyper-parameters to evaluate the performance of each and then use the parameters it found to be the best when making the predictions.

#### Variance Threshold

The variance threshold is a feature selection technique that takes in a specific variance amount and will identify all feature variables that are not meeting the threshold and remove them. This allows the model to only perform predictions on features that have a variance up to a specific amount.

#### KBest

The KBest (or SelectKBest) is a feature selection technique that allows for the selection of a specific amount of feature variables to be used when performing the predictions on the target variable (Sale Price). Specifically, I am using the f_regression with KBest which will score the selected features and use the optimal ones in the model.

#### Ridge

Ridge regression is a regularized technique that allows the model to take on more weight related to variance. This technique is used when we have strong multicollinearity across our selected feature variables. The Ridge regression imposes a penalty on the estimates to those that were identified as performing the worst in the model by taking the sum of the square coefficients. In this technique a feature will never be zeroed out but just be brought closer and closer to zero to help the model predictions.

# Conclusion

With the GridSearch w/Ridge model I was able to get an explanation about what features are the most influential to a homes sale price in Ames, Iowa. The following features are two of the most heavily influenced features:

- Overall Quality
- Square footage above ground

When examining these two features by neighborhood there are two neighborhoods that clearly are leading all other neighborhoods in these areas. Those neighborhoods are:

- Stone Brook
- North Ridge Heights

What can also be observed is that the above two neighborhoods are also leaders in the overall average sale price of homes in the entire city. Knowing this I can conclude that where you live, or in what neighborhood you reside, within the city of Ames, Iowa will influence the price of your home.
