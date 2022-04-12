# CIND820Ames
Big Data Analytics Project for CIND820
## Abstract
Alongside food and water, housing is a basic human necessity.  It is then a concern that housing is increasingly becoming a scarce commodity.

Canada is experiencing an incredibly tight property market with demand and, consequently, prices soaring.  While select large urban real estate markets such as Vancouver and Toronto had already been experiencing significant price pressure, elevated prices are increasingly becoming the norm across much of the country. According to the CREA(2022), year-over-year home prices across the country reached a record high of 26.6% in December 2021 and this type of upward price movement is expected to continue.

In this context, being able to accurately assess and predict real estate prices is of paramount importance.  This is certainly true for prospective home buyers who need to make every penny count.  Such insight is also in high demand from investors and developers who are under intense pressure to find value.  From a very different perspective, public agencies and policymakers at all levels of government have a pressing need to be able to predict housing prices - especially in the context of the current housing shortage.

The main research question that this project seeks to answer is: Which current analytical methods and machine learning techniques perform best in predicting housing prices?  A secondary question is whether more novel machine learning methods are a significant improvement on traditional regression methods and if so in what ways?

The themes that this project deals with are regression and predictive analytics. The methods that I propose to compare include: multiple linear regression (baseline), random forests, gradient boosting and artificial neural network.  Prior to model comparison, a process of feature selection will likely be necessary using techniques such lasso regression.  

The main tools that will be used for the project will be Python along with their various libraries such as glmnet, pandas, sci-kit learn, and XGBoost.

## Data Understanding
### Data Set
To explore this question, I will use the Ames Housing dataset.  This feature rich dataset documents housing price in Ames Iowa from 2006 to 2010.  It was assembled as a modern alternative to the well-known Boston Housing dataset that had long served as benchmark to assess linear regression models (De Cock, 2011).  The data set contains just over 2900 observations and has 82 features.  The dataset is very well documented and the various features in the dataset are straightforward.  Furthermore, it is possible to access the records of the City of Ames Assessor’s Office to help clarify and better understand the data.

### Literature Review
I conducted a thorough review of the literature on traditional hedonic approaches to property pricing in comparison with the development of machine learning models to property price prediction.
I found that, currently, machine learning models do tend to outperform traditional hedonic methods based on multiple linear regression.  There are, however, some drawbacks to machine learning models such as the relative lack of explanatory power.  It also seems quite clear that while some methods (e.g. decision tree) tend to underperform relative to other machine learning models, there is currently no definitively best ML model for property price prediction.
Lastly, I was surprised to learn that formal academic literature that concentrates on the Ames Housing Data Set is limited even though this data set is clearly very popular among data science practitioners and students.
## Data Preparation I
The initial stage of data preparation focused on cleaning up the data and correcting discrepancies which was necessary to get an accurate picture of the date during the exploratory phase.
-	Identified Na values in the dataset and changed them to the appropriate values
-	Resolving errors and discrepancies in the dataset and checking data set against assessor records where necessary
-	Recoding ordinal variables that were not in numerical format
-	Changed nominal variables that were labelled with numbers

## Exploratory Data Analysis
In the exploratory analysis, I focused on the relationships between the target variable and the rest of the dataset as well as interrelations between independent variables.
-	Created a series of scatter plots and box plots that illustrated the relationship between Sale Price and a variety of numerical and categorical variables that were assumed to be important
-	Checked the frequency distribution of the target variable (Sale Price) via a histogram
-	Created a set of histograms for all numeric variables to check frequency distributions
-	Generated several correlation matrices to examine correlation with Sale Price and checked for problems of multicollinearity
-	Examined a pairwise plot of Sale Price and top correlated variables

## Data Preparation II
As a result of the exploratory phase, it became clear that a few additional steps needed to be taken to proceed with the data preparation.  This involved removing a few outliers and performing a log transformation.  Finally, it was necessary to recode categorical variables and standardize numerical variables before running any algorithms on the data.
-	Removed several outliers
-	Created a variable, Total Indoor Square Footage, which combined Above Grade Living Area Square Footage and Total Basement Square Footage
-	Performed a log transformation on target variable and those independent numerical variables that were significantly skewed
-	Performed one-hot encoding on categorical variables
-	Standardized all data to create similar scale for all variables

## Feature Selection
-	Created a basic feature that included independent variables most highly correlated with Sale Price while removing variables with high collinearity.
-	Used Random Forest Regressor via sklearn feature.selection’s SelectFromModel module and tuned hyperparameters.
-	Created a visualization of the results and examined the 71 features that were selected
-	Used Lasso Regressor via sklearn feature.selection’s SelectFromModel module and tuned model
-	Created a visualization of the results and examined 20 features that were selected.
-	[Further fine tuning/comparison required]

## Initial Multiple Linear Regression Model & Lasso Regularized Regression
This stage of modelling is very much an extension of the preparation/exploratory phase of the project.  It is mainly undertaken in order to test the viability of running models on the data and testing feature selection.
-	Discovered that a basic multiple linear model with all 81 features was not feasible as it did not result in a viable predictive model
-	Preliminary base multiple linear regression model using a set of 16 basic features
-	Preliminary multiple linear regression model with features selected by random forest selector
-	Preliminary multiple linear regression model with features selected by Lasso regression selector

## Main Modelling
1.-Multiple Linear Regression
The multiple linear regression model was included here so as to have a linear model that uses the same feature set as all other models.  This actually proved somewhat problematic.  When some slightly larger feature sets were used, the multiple linear model again broke as it did when all features were included.  However, the linear model performs extremely well with the feature set that was settled upon.  Indeed, it is somewhat surprisingly one of the top performing models finishing marginally behind Lasso Regression in terms of model effectiveness while clearly outperforming in terms of efficiency.  Although there are, in fact, stability issues with the linear model, in the case of this particular feature set, there was no large difference as the number of k folds was changed during cross-validation.

|Metrics        |K10|
|---------------|---|
|AdjR2 CV Test  |0.904509|
|AdjR2 CV Train |0.905381|
|MAE CV Test    |0.08071 |
|MAE CV Train   |0.083152|
|RMSE CV Test   |0.10596 |
|RMSE CV Test   |0.113837|

2.-Lasso Multiple Regression
The results show that, as expected, Lasso regression is very effective.  In fact, it is the best model in terms of all effectiveness metrics, very narrowly surpassing Multiple Linear Regression.  On the other hand, it performs significantly worse than plain linear regression in terms of time efficiency but this is likely largely down to the cross-validation that is built into the model.  It is also exceedingly stable.

|Metrics        |K10|
|---------------|---|
|AdjR2 CV Test  |0.905079|
|AdjR2 CV Train |0.905401|
|MAE CV Test    |0.080352|
|MAE CV Train   |0.083043|
|RMSE CV Test   |0.10559|
|RMSE CV Test   |0.113817|

3.-Decision Tree Regressor
The results demonstrate that the Decision Tree Regressor was the poorest performing model in the study in terms of effectiveness. It managed only 0.1695 RMSE, 0.1267 MAE, and 0.7597 Adjusted R2 on the test data.  The model, though, is quite efficient.  It has one of the lowest time-costs at an average 8.118ms per loop of any of models in the study except for plain Multiple Regression. Though its results were fairly uniform, the Decision Tree Regressor was comparatively one of the more unstable models in terms of results changing as the k increased for cross-validation.

|Metrics        |K10|
|---------------|---|
|AdjR2 CV Test  |0.759655|
|AdjR2 CV Train |0.827071|
|MAE CV Test    |0.126762|
|MAE CV Train   |0.112462|
|RMSE CV Test   |0.169452|
|RMSE CV Test   |0.154893|

4.-Random Forest Modelling
The results of the random forest model were quite good with a RMSE of 0.1241 and a MAE of 0.0885 on the test data.  This performance is not at all terrible and within the range of the best performing models.  Nevertheless, the random forest model was still outperformed by a linear regression model that simply used highly correlated variables.  What was particularly interesting is that the Random Forest Regressor actually underperformed a linear model that used features selected via a random forest selector.  This suggests that the feature selection element of the random forest model was sound, but that regression tree models were perhaps particularly ill-suited to the particular data set.  The results of the random forest were especially disappointing as it is also quite time inefficient.  Random forest was a very stable model only slightly bested by Lasso

|Metrics        |K10|
|---------------|---|
|AdjR2 CV Test  |0.872414|
|AdjR2 CV Train |0.893476|
|MAE CV Test    |0.088548|
|MAE CV Train   |0.085935|
|RMSE CV Test   |0.124122|
|RMSE CV Test   |0.121109|

5.-Gradient Boost(XPG)
XGBoost is one of the best performing models overall.  While it very slightly bested the Multiple Linear Regression and Lasso models on all measures of effectiveness for the training data, it was slightly worse with the actual test data.  Even so, the difference in scores for training and test data was very small indicating that overfitting is not a major problem.  In terms of efficiency, as an ensemble model it did require more time than the Decision Tree Regressor, Lasso, and Multiple Linear Regression models.  Once the number of estimators was reduced, XGBoost did outperform the random forest model.  In terms of stability, the XGBoost model had no significant problems.

|Metrics        |K10|
|---------------|---|
|AdjR2 CV Test  |0.892479|
|AdjR2 CV Train |0.908649|
|MAE CV Test    |0.083682|
|MAE CV Train   |0.08027|
|RMSE CV Test   |0.112065|
|RMSE CV Test   |0.111700|
6.-Artificial Neural Network Perceptron(Keras)
The results make clear what had been suspected: an ANN model is not the most appropriate method for the Ames Housing dataset.  The Perceptron was the second worst performing model behind only the Decision Tree Regressor model.  That said its effectiveness results were not terrible and within a reasonable distance of better performing models.  However, the efficiency cost in terms of processing time was by far the highest of any model even using the additional processing power of a graphic processing unit.  It also proved to be the least stable of the models.

|Metrics        |K10|
|---------------|---|
|AdjR2 CV Test  |0.821829|
|AdjR2 CV Train |0.872189|
|MAE CV Test    |0.106024|
|MAE CV Train   |0.09726|
|RMSE CV Test   |0.143286|
|RMSE CV Test   |0.132625|


## Conclusions & Areas for Future Research
In the case of the Ames dataset, the results of this study show that linear multiple regression particularly in its advanced Lasso form outperforms the machine learning models in terms of effectiveness, efficiency and stability.  Such a comparison must, however be kept firmly in context – the context of this specific dataset.  It was a relatively small dataset with less than 3000 observations and significant portions of the data displayed fairly strong linear relationships to the target variable.  Lasso regression was particularly well-suited to the problem of a large number of features.  It is really striking how well plain linear regression performed.  In this particular application, one could possibly argue that no more complex model was really needed.  Nevertheless, it must be noted that the multiple regression model could not handle the dataset when all features were included and it performed best when supplied with a selection of features using more advanced methods.  That said, the results here show that one must be careful about assuming that the newest and most advanced techniques in the data science arsenal are superior in every case.  There are still and likely will be for some time, use cases that clearly call for a multiple regression model.

Despite the strong performance of linear regression, the results also showed that machine learning models can certainly be effective in predicting housing prices.  All the models investigated here produced strong predictive results and even the poorest performers were not extremely far off from the results of the best performing models.  Gradient Boosting via XGBoost proved to be especially effective when compared to other machine learning models.  It had the strongest performance in terms of all the measures of effectiveness on both the training and test sets.  It also scored impressively in terms of efficiency even though it is a more complex ensemble model.  In contrast, the Decision Tree Regressor had the worst effectiveness scores but was the top performer aside from the plain linear model in terms of efficiency.  The Random Forest Regressor model was, somewhat surprisingly, one of the poorer performing models finishing just behind the stronger performers in terms of effectiveness and very clearly one of the worst performers in terms of time efficiency.  The Artificial Neural Network model also performed quite poorly though its results improved dramatically after some optimization.
Again, all these results must be kept in context.  In this instance, advanced machine learning models were ill suited to the use case.  Machine learning models such as Random Forest, Gradient Boosting and especially Artificial Neural Networks would likely perform better when supplied with much, much larger datasets.   As well, the real strengths of these advanced models is that they are able to do precisely what linear models struggle with – deal effectively with non-linear relationships in the data.  In many cases, one would want to utilize one of these more advanced models given that linearity cannot easily be assumed given that these models perform quite well on linear data and excel when the data is more complex.
At first glance, the findings here seem to run counter to much of our literature review which presented a strong case that machine learning models were generally better than traditional hedonic models relying on linear regression.  However, aside from being a bit too dismissive of linear regression (especially for simple scenarios), the real conclusion of the literature review was that there is no one single best machine learning model in terms of housing price prediction.  This fits well with the results presented in this study.  It is true that Gradient Boosting is generally a very strong performer.  It is also true that Artificial Neural Network models are at the cutting edge of all kinds of interesting and innovative techniques using a wide variety of different kinds of data.  On the other hand, in spite of being less high powered in terms of price prediction, the time efficiency of regression trees along with their ability to handle non-linear data might make them the ideal choice if one is looking for a simple model capable of processing tons of data with a low overhead cost.  
The key conclusion then is that context matters.  

## Contents of Repository
-	Read.me File
-	Python/JuypterNotebook File for Intial Code
-	Python/JupyterNotebook File for Final Code
-	HTML copies of both Intial & Final notebook files
-	Dataset in Excel(.xls) format
-	Results in Excel (.xlsx) format
-	Image Folder
