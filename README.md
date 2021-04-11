# Module 3 Final Project - Predicting the Condition of Waterpoints in Tanzania


## Overview of the Repository
```
index.ipynb             
# Jupyter notebook containing code for data discovery, EDA and a number of models, with improving accuracy, that aim to predict the condition of the waterpoints.

presentation.pdf        
# A non-technical presentation of the project findings

regional_choropleth.html
# 

└── source-data 

        training-set-values.csv                 
        # Raw "training" dataset of 59,400 Tanzanian waterpoints containing the following information for each waterpoint:
            * id
            * amount_tsh
            * date_recorded
            * funder
            * gps_height
            * installer
            * longitude
            * latitude
            * wpt_name
            * num_private
            * basin
            * subvillage
            * region
            * region_code
            * district_code
            * lga
            * ward
            * population
            * public_meeting
            * recorded_by
            * scheme_management
            * scheme_name
            * permit
            * construction_year
            * extraction_type
            * extraction_type_group
            * extraction_type_class
            * management
            * management_group
            * payment
            * payment_type
            * water_quality
            * quality_group
            * quantity
            * quantity_group
            * source
            * source_type
            * source_class
            * waterpoint_type
            * waterpoint_type_group

        training-set-labels.csv
        # Raw "training" labels, denoting the functional status of the Tanzania waterpoints, corresponding to the waterpoint data provided in `training-set-values.csv`
        
        test-set-values.csv                 
        # Raw "test" dataset of Tanzanian waterpoints         

└── other-data

        tanzania-regions.geojson
        # GeoJSON file containing shape data for the administrative regions within Tanzania for use in the choropleth.



```

## Business Case and Brief

A property development company in Washington State wants to better understand the factors that influence the sale price of a property.

They are keen to use statistical modelling techniques to assist their decision making processes and better inform the planning, design and marketing of new build and / or renovated properties within the King County area.

Whilst we recognise that certain influencing factors are beyond the control of the developers, it is useful to understand their effect on the data.


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