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
-	Developed a base multiple linear regression model using a set of 16 basic features
-	Developed a multiple linear regression model using 71 features selected by random forest selector
-	[Need to create multiple linear regression model using 20 variables from lasso selector]
-	Developed a Lasso regression model

## Main Modelling
-Random Forest Modelling
[To Be Completed]
-Gradient Boost(XPG) Modelling
[To Be Completed]
-Artificial Neural Network Modelling
[To Be Completed]

## Conclusions & Areas for Future Research
[To Be Completed]

## Contents of Repository
-	Read.me File
-	Python/JuypterNotebook File for Intial Code
-	Python/JupyterNotebook File for Final Code
-	HTML copies of both Intial & Final notebook files
-	Dataset in Excel(.xls) format
-	Results in Excel (.xlsx) format
-	Image Folder
