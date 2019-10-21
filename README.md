# svclassifier

# Problem Statement
Using the [NASA Kepler Exoplanet Search Results](https://www.kaggle.com/nasa/kepler-exoplanet-search-results), fit a predictive model to
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
7.  We consider the possibility of dimension reduction with principal component analysis.
8.  Decision tree classifiers are considered. 

# Summary
[Jupyter notebook via nbviewer](https://nbviewer.jupyter.org/github/douglasdrake/svclassifier/blob/master/svclassifier.ipynb "Jupyter notebook").

The linear support vector classifier acheives an accuracy of 90% on the training data and 89% on the test data.  The grid search still selects the linear kernel for the classifier when allowed to choose among linear, polynomial, radial-basis, and sigmoidal basis functions.  

Principal component analysis suggests that we could reduce the dimensionality from 31 numerical predictors to 12.  We do not fit models with the PCA reduction at this time; however, plots with the principal component directions do indicate some separation in the class distributions.

The tree decision classifier did not fit as well as the linear support vector classifier; it made more errors on the test data with respect to `CANDIDATE` and `CONFIRMED` classes.  Both classifiers performed equally with high recall and precision for the response class `FALSE POSITIVE`.  

We were able to look at feature importances for the decision tree classifier.  The three most important predictors were `koi_srad_err1`, `koi_srad`, and `dec`.  The first two are estimates of the error and the photospheric radius of the star; the last is a KIC parameter, declination.


