# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 5: Predicting Global Crop Yield for World Hunger

## Problem Statement

You are a team of data scientists hand-picked by the United Nations in order to help come up with a machine learning model to help the UN reach its Zero-Hunger goal by 2030. Currently there are nearly 1 in 8 people who do not have enough food to lead a healthy life. 870 million people do not have enough food to eat. Currently there are 7.9 billion people on the planet. To make things more difficult, the global population has been increasing steadily and is expected to reach 8.5 billion people. Therefore, with some back-of-envelope calculations, you can see that in order to end world hunger by 2030, the UN needs to come up with a strategy for nearly 940 million people at the current rate or up to 1.5 billion if we add all the new people projected to be on the planet as well as the existing number of hungry individuals. Either way, we are talking about nearly 1-1.5 billion people lacking sufficient food. For this reason, your team has been tasked with analyzing global historical data related to crop yields and figuring out how the citizens of the world can use machine learning and data science to understand the most important factors related to crop yield, temperature, rainfall, irrigation, and pesticides.

### Project Goal:

1. Create a model that successfully predicts Crop yield given various basic features related to agriculture on a global scale using longitudinal data

2. Using this data and these models, can you predict which crops will be the most important crops to target worldwide production and in which continents? What about in which countries?

## Executive Summary:

For this work, our main data set was pulled from FAOSTAT (by the Food and Agriculture Databank of the FAO). Our goal was to build various types of regression models in order to predict crop yield, as we felt this parameter is incredibly important to help solve the global hunger crisis and to support the UN mission of ending world hunger by 2030. We first needed to clean the data set by dropping null values and merging available data sets. In the Exploratory Data Analysis, we visualized the cleaned data in order to get a better sense of how crop yield related to other features in the data set. In the modeling phase, we tested various models on two feature sets and prioritized the strongest model that predicted yield for this data set by comparing R2, MAE, RMSE, and MSE scores. We concluded that Adaboost Regressor was the best model and we were able to get a 0.96 R2 score for our testing set. We were able to find which features were most predictive of our target variable, crop yield such as: 'crop potatoes','area' (in hectares), and 'fertilizer use.' Our model was succesfully able to predict crop yield in a global data set. We were able to determine that potatoes have a high yield, but low levels of production, while other crops such as rice and wheat have a high level of production, despite decreasing harvested area, indicating higher agronomic efficiency.

## Data Sources

### FAO Data

Our dataset was derived from FAOSTAT(The Food and Agriculture Databank of the FAO). [Dataset Link](https://www.fao.org/faostat/en/#home)

FAO, the Food and Agriculture Organization of the United Nations, is a specialized agency of the United Nations that leads international efforts to defeat global hunger. With over 194 member states, FAO works in over 130 countries worldwide. [About FAO](https://www.fao.org/about/en/)  

FAOSTAT provides free access to food and agriculture data for over 245 countries and territories and covers all FAO regional groupings from 1961 to the most recent year available. FAOSTAT data are organized within the following domains:
- Production
- Food Security and Nutrition
- Food Balances
- Trade
- Prices
- Land, Input and Sustainability
- Population and Employment
- Investment Macro-Economics Indicators
- Climate Change
- Forestry

### Data Dictionary

|                | Type    | Description                               | Example      |
|----------------|---------|-------------------------------------------|--------------|
| Area_code      | float64 | FAO code associated to the Country        | 1            |
| Country        | object  | Country name                              | Albania      |
| Item_code      | float64 | FAO code associated with the crop         | 44           |
| Crop           | object  | Name of the crop                          | Wheat        |
| Year           | float64 | Calendar year                             | 1961         |
| Area_ha        | float64 | Harvested area for the crop in ha         | 350000       |
| Yield_hg_ha    | float64 | Yield per crop in hg/ha                   | 14000        |
| Value_N_tonnes | float64 | Total N applied in the country in tonnes  | 1000         |
| Value_P_tonnes | float64 | Total P applied in the country in tonnes  | 100          |
| Value_K_tonnes | float64 | Total K applied in the country in tonnes  | 50           |
| pop_unit       | object  | Unit of pop_value (1000 person)           | 1000 persons |
| pop_value      | float64 | Number of people to be multiplied by 1000 | 9169.41      |


### Staple Crop Selection

A crop is a plant that can be grown and harvested for food or profit. By use, crops fall into six categories: food crops, feed crops, fiber crops, oil crops, ornamental crops, and industrial crops [(Source)](https://www.nationalgeographic.org/maps/wbt-staple-food-crops-world/).   For our research we to selected the most important food crops based on their share of global caloric intake from all sources.  The ranking was based on data from the WorldAtlas ranking [(Source)](https://www.worldatlas.com/articles/most-important-staple-foods-in-the-world.html), wikiepedia [(Source)](https://en.wikipedia.org/wiki/Staple_food) and FAO [(Source)](https://www.fao.org/3/u8480e/u8480e07.htm).  We also included barley as it is the fourth most important cultivated cereal in the world [(Source)](https://www.croptrust.org/).  The selected food crops are:

- Maize
- Potato
- Rice, paddy
- Wheat
- Sorghum
- Cassava
- Barley
- Soybeans
- Yams

### Fertilizer

For each Crop, we downloaded harvested area and yield data from 1961 through 2019 for all the countries from which FAO collects data.  Unfortunately, there are no data on the type and quantity of fertilizer used for each of crop we selected.  Since fertilizer is the most important input in crop production we decided to use fertilizer data for the entire country as a metric of the input for each crop.    We used data for the three macronutrients : nitrogen total (N), phosphate total (P) and potash total K.  Data for K are not as complete as those for N and P, in many cases data prior to 1970 is non-existent.

### Population

Data on population were download for each country selected.  Values are for 1000 person

### Data Import and Handling

All dataset were downloaded as csv.   To merge datasets unique keys were created.  When merging data for crop and yield the key was “CountryYearCrop”.  To merge fertilizer and population data the key was “CountryYear”.  After import and the merge columns were renamed for ease of use.  Redundant columns were eliminated.

## MODELING

The modeling was done using the dataset created after initial data cleaning and EDA, it centered around using two feature sets to train and test the model. These two feature sets were defined as either having crop and continent dummy columns or having crop, continent, and country dummy columns. The distinction between these two were further heightened when looking at the total feature size, while the first feature set only had 19 features, the second feature set which included dummy columns for countries had 189 columns.

We used seven different models for each of these two feature sets. These models were Linear Regression, K-Nearest Neighbors, Decision Tree Regressor, Bagging Regressor, Random Forest Regressor, Ada-Boost Regressor, and a Gradient-Boost Regressor. Through numerous trials, we were able to determine that for both feature sets, Ada-Boost Regressor had the greatest overall performance.

## CONCLUSION

- A machine learning model has value in predicting crop yield and total production

- Our models can successfully isolate the most important factors for predicting crop yield

- Crop Yield is generally increasing for all major crops, even while harvested area decreases

- Crop yield will need to be considered with other types of metrics (crop yield / capita, total production, total
production per capita) to get a fuller picture of the global hunger crisis

- More agronomical data will be necessary to correctly predict each single crop locally

## SOFTWARE REQUIREMENTS
Programming language used: Python

Packages prominently used:

Pandas: For data structures and operations for manipulating numerical tables

Numpy: For work on large, multi-dimensional arrays, mathematical functions, and matrices.

Seaborn: Data visualization built on top of Matplotlib and integrates well with Pandas.

Matplotlib: The base data visualization and plotting library for Python, seaborn is built on top of this package

Scikit-Learn: Scikit-learn is a free software machine learning library for the Python programming language. Specific Scikit-Learn libraries used are neighbors, ensemble, pipeline, model selection, metrics, linear model, and pre-processing