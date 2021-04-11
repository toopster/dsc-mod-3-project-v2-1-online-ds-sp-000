# Module 3 Final Project - Predicting the Condition of Waterpoints in Tanzania


## Overview of the Repository
```
index.ipynb             
# Jupyter notebook containing code for data discovery, EDA and a number of models, 
with improving accuracy, that aim to predict the condition of the waterpoints.

presentation.pdf        
# A non-technical presentation of the project findings

regional_choropleth.html
# 

└── source-data 

    ├── training-set-values.csv                 
        # Raw "training" dataset of 59,400 Tanzanian waterpoints.

    ├── training-set-labels.csv
        # Raw "training" labels, denoting the functional status of the Tanzania 
        waterpoints, corresponding to the waterpoint data provided in
        training-set-values.csv.   

    ├── test-set-values.csv                 
        # Raw "test" dataset of 'unseen' Tanzanian waterpoints to be used to predict
        their functional status.   

└── submission-data 

└── other-data

        tanzania-regions.geojson
        # GeoJSON file containing shape data for the administrative regions within Tanzania for use in the choropleth.



```

## Business Case and Brief

Did you know 2.2 billion people globally do not have safely managed drinking water services?

Water is an essential of life, yet millions around the world still don’t have access to clean water. 
One of the most common causes of death in the developing world is drinking dirty and diseased water.

Tanzania has a water and sanitation crisis. Only 60% of the population of 61 million have access to
an improved source of safe water (protected from contamination), and 34% of the population has access to improved sanitation. 
The demand for both water and sanitation is high.

Water wells provide clean water for years. In rural areas, they are a lifeline for the inhabitants as
this may be the only source of potable water.

Using data from Taarifa and the Tanzanian Ministry of Water, can you predict which pumps are functional, 
which need some repairs, and which don't work at all? This is an intermediate-level practice competition. 
Predict one of these three classes based on a number of variables about what kind of pump is operating, 
when it was installed, and how it is managed. A smart understanding of which waterpoints will fail can improve 
maintenance operations and ensure that clean, potable water is available to communities across Tanzania.

The goal is to predict the operating condition of a waterpoint for each record in the dataset.


## Approach

As outlined in the [Jupyter Notebook](index.ipynb) included in this repository, the approach constituted two main parts:

1. Initial **Exploratory Data Analysis** to review and validate the data fields available in the `training-set-values.csv` dataset and understand each feature and their relationships both with each other and with the target variable, `price`.  The notebook contains several visualisations that are used in the [non-technical presentation](presentation.pdf) but also a choropleth map of average house price by zipcode.  Unfortunately the map does not appear inline within the notebook but in a [separate file](zipcode_choropleth.html).

![Average House Prices in King County 2014-15 by Zip Code](house-price-choropleth.png)

![Number of House Sales in King County 2014-15 by Zip Code](number-of-house-sales-by-zipcode.png)

2. The creation, refinement through iteration, validation and evaluation of a **Multivariate Linear Regression Model** including the use of stepwise feature selection, that highlights the influencing features and creates a prediction model for house prices in King County.


## Conclusions

The [Jupyter Notebook](index.ipynb#linear-regression) contains the details of each iteration of the linear regression model.  It was possible to create a [multivariate linear regression model](index.ipynb#model-v10) that, at first glance, produced a good predictive model with an R-Squared value of **0.843**.  However, on closer inspection, p-values for certain predictors are above 0.05 and therefore are not within acceptable bounds and the Jarque-Bera test score is too high suggesting that the distribution of residuals is not normal thereby not meeting one of the assumptions of linear regression.

After using [stepwise feature selection](index.ipynb#model-v11) and a more [manual approach](index.ipynb#model-v12) to refine the model further a satisfactory model was achieved with a R-Squared value of **0.559** but that had all predictors with p-values less than 0.05 and has a JB test score of **5.853**.

This final model was evaluated using both [train-test split](index.ipynb#model-evaluation-train-test-split) and [cross validation](index.ipynb#model-evaluation-cross-validation) with acceptable results.

The model shows the following impact on house prices in King County.

House prices tend to increase with increases in:
* Living Space (but this fluctuates between zip codes)
* Location (Waterfront)
* View

House prices tend to decrease with increases in:
* Lot Space



## Requisite Python Libraries

The following python libraries have been used as part of this project:

* [Pandas](https://pandas.pydata.org/)
* [NumPy](https://numpy.org/)
* [Seaborn](https://seaborn.pydata.org/)
* [Matplotlib](https://matplotlib.org/)
* [datetime](https://docs.python.org/3/library/datetime.html)
* [Folium](https://python-visualization.github.io/folium/)
* [JSON](https://docs.python.org/3/library/json.html)
* [scikit-learn](https://scikit-learn.org/)
* [statsmodels](https://www.statsmodels.org/stable/index.html)
* [SciPy](https://www.scipy.org/)