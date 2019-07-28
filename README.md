# svclassifier

# Problem Statement
Using the [https://www.kaggle.com/nasa/kepler-exoplanet-search-resultsNASA](Kepler Exoplanet Search Results), fit a predictive model to
classify a Kepler Object of Interest (KOI) using the available predictors.

# Methods Used
1.  The data is first cleaned by removing redundant features.  A preliminary look at the data indicates that skewness and heavy-tails 
in the predictor distributions will need to be addressed.
2.  We split the data into a training set and test set; the splitting method stratifies on the class of the response to allow for similar proportions
of each response category to be present in the training and test data.
3.  We consider plots to visualize the ability of single predictors and pairs of predictors to classify the response.  We also consider how correlated
the predictors are with each other.
4.  Using Scikit-Learn's transformation/pipeline features, we transform the numerical predictors using Yeo-Johnson transformations before applying 
a MinMax scaling.  Yeo-Johnson transformations are a family of power transformations that can account for negative input values.  
5.  A linear support vector classifier is used on the training data.
6.  We consider a range of parameter values for the support vector classifier with a pair of cross-validated grid searches. 

# Summary
The linear support vector classifier acheives an accuracy of 90% on the training data and 89% on the test data.  The grid search still selects the linear kernel for the classifier when allowed to choose among linear, polynomial, radial-basis, and sigmoidal basis functions.  