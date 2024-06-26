# Power Outages: An Investigative Analysis

### by Jet Yue and Namitha Vishnupad
#### Website Link: https://jetyue04.github.io/Power_Outages_Impact/

# Introduction

Welcome to our analysis of power outages across the United States. The core of this project's data consists of detailed records of major power outages in the United States, which contains information about the causes of these outages, their duration, the number of people/consumers impacted, and various other socio-economic factors related to the impacted regions. 

<br>

<center><img src = "https://i.ytimg.com/vi/eSmUwjGs738/maxresdefault.jpg" width = 500></center>

Power outages are significant events, and can disrupt daily life, impact economic activities, and potentially pose risks to health and safety - especially ones on larger scales. We aim to answer the question of finding the characteristics of major power outages with high severity, and whay risk factors an energy company might want to look into when predicting the location/severity of its next major power outage.


And we know it is hard to find a single answer to this question. So, we have narrowed our approach to be slightly more specific, with the following research question:

#### Is there a significant difference in the mean outage duration between major power outages caused by severe weather, and major power outages caused by intentional attacks?

This question aims to uncover whether the nature of the cause of the outage - whether it is natural or human induced, affects the duration of the power outage. The answer could potentially influence how resources are allocated for outage prevention, as well as inform strategies for improving the resilience of power infrastructure.


Before we delve into our project, here is a brief summary of our dataset:

The working dataset we are using has <b><span style="color:red">**1536 rows**</span></b> and <b><span style="color:blue">**56 columns**</span></b>. 

Shortly put - this is a lot of data 😬. 

For our approach, we have compiled a list of the data we feel is most relevant to our research question -


- OUTAGE.DURATION: Duration of the power outage in minutes.
- CAUSE.CATEGORY: Primary category of the cause of the outage (e.g., severe -weather, intentional attack).
- OUTAGE.START.DATE: Date when the outage started.
- OUTAGE.RESTORATION.DATE: Date when power was restored.
- CUSTOMERS.AFFECTED: Number of customers affected by the outage.
- U.S._STATE: State in which the outage happened
- CLIMATE.REGION: Climate region of the outage location.
- CLIMATE.CATEGORY: The climate conditions corresponding to previous years, categorized as "Warm," "Cold," or "Normal"
- RES.SALES, COM.SALES, IND.SALES: Electricity consumption patterns by residential, commercial, and industrial sectors.
- TOTAL.SALES: Total electricity sales in the affected area.
- PC.REALGSP.STATE: Per capita real Gross State Product.
- POPULATION: Population of the affected area.
- HURRICANE.NAMES: Although we don't necessarily care about the name of the hurricanes, the presence/absence of a hurricane can provide information regarding the cause and severity of the power outage


# Data Cleaning and Exploratory Data Analysis
Below, we have displayed the first 5 rows of the original dataset:


|   variables |   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | OUTAGE.START.DATE   | OUTAGE.START.TIME   | OUTAGE.RESTORATION.DATE   | OUTAGE.RESTORATION.TIME   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND |
|------------:|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:--------------------|:--------------------|:--------------------------|:--------------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|
|         nan |   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | 2011-07-01 00:00:00 | 17:00:00            | 2011-07-03 00:00:00       | 20:00:00                  | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |       11.6  |        9.18 |        6.81 |          9.28 | 2.33292e+06 | 2.11477e+06 | 2.11329e+06 |   6.56252e+06 |      35.5491 |      32.225  |      32.2024 |         2308736 |          276286 |           10673 |           2595696 |        88.9448 |        10.644  |       0.411181 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |      5348119 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|         nan |   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | 2014-05-11 00:00:00 | 18:38:00            | 2014-05-11 00:00:00       | 18:39:00                  | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |       12.12 |        9.71 |        6.49 |          9.28 | 1.58699e+06 | 1.80776e+06 | 1.88793e+06 |   5.28423e+06 |      30.0325 |      34.2104 |      35.7276 |         2345860 |          284978 |            9898 |           2640737 |        88.8335 |        10.7916 |       0.37482  |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |      5457125 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|         nan |   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | 2010-10-26 00:00:00 | 20:00:00            | 2010-10-28 00:00:00       | 22:00:00                  | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |       10.87 |        8.19 |        6.07 |          8.15 | 1.46729e+06 | 1.80168e+06 | 1.9513e+06  |   5.22212e+06 |      28.0977 |      34.501  |      37.366  |         2300291 |          276463 |           10150 |           2586905 |        88.9206 |        10.687  |       0.392361 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |      5310903 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|         nan |   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | 2012-06-19 00:00:00 | 04:30:00            | 2012-06-20 00:00:00       | 23:00:00                  | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |       11.79 |        9.25 |        6.71 |          9.19 | 1.85152e+06 | 1.94117e+06 | 1.99303e+06 |   5.78706e+06 |      31.9941 |      33.5433 |      34.4393 |         2317336 |          278466 |           11010 |           2606813 |        88.8954 |        10.6822 |       0.422355 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |      5380443 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|         nan |   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | 2015-07-18 00:00:00 | 02:00:00            | 2015-07-19 00:00:00       | 07:00:00                  | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |       13.07 |       10.16 |        7.74 |         10.43 | 2.02888e+06 | 2.16161e+06 | 1.77794e+06 |   5.97034e+06 |      33.9826 |      36.2059 |      29.7795 |         2374674 |          289044 |            9812 |           2673531 |        88.8216 |        10.8113 |       0.367005 |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |      5489594 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |


As you can see, there is a lot of missing data, and it's not the most interpretable data. Therefore, we cleaned the data with the following steps:

In the original dataset, there are several rows in the excel sheet encompassing a description of the data. We removed those rows before importing it into our notebook.
1. Combine the 'OUTAGE.START.DATE' and 'OUTAGE.START.TIME' columns into a single string for each row, handling missing values by replacing them with empty strings.
2. Convert the combined date-time strings into datetime objects, coercing invalid entries to NaT values (Not a Time)
3. Created new column called 'is_hurricane' to indicate if outage is associated with a hurricane. This is done by checking if hurricane name is missing.
4. Extracted columns of interest
5. We then checked for unreasonable values:
    - Duration, Demand Loss and Customer affected should not be 0
    - all other columns's value are checked
    - REPLACE WITH NAN VALUES

In summation: the data cleaning steps transformed raw data into a structured and analyzable format. By filling missing values, combining date and time columns, calculating outage durations, and standardizing categorical data, we ensured that the dataset is ready for meaningful analysis. These steps were essential for achieving accurate and reliable insights into the characteristics and severity of major power outages, ultimately aiding in the identification of risk factors for future outages.

#### The first 5 rows of our cleaned data:

|   YEAR |   MONTH | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     | CLIMATE.CATEGORY   |   ANOMALY.LEVEL | OUTAGE.START        | OUTAGE.RESTORATION   |   OUTAGE.DURATION | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   TOTAL.PRICE |   TOTAL.SALES |   POPPCT_URBAN |   POPDEN_URBAN |   AREAPCT_URBAN | is_hurricane   |
|-------:|--------:|:--------------|:--------------|:-------------------|:-------------------|----------------:|:--------------------|:---------------------|------------------:|:-------------------|:------------------------|-----------------:|---------------------:|--------------:|--------------:|---------------:|---------------:|----------------:|:---------------|
|   2011 |       7 | MN            | MRO           | East North Central | normal             |            -0.3 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |              3060 | severe weather     | nan                     |              nan |                70000 |          9.28 |   6.56252e+06 |          73.27 |           2279 |            2.14 | False          |
|   2014 |       5 | MN            | MRO           | East North Central | normal             |            -0.1 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |                 1 | intentional attack | vandalism               |              nan |                  nan |          9.28 |   5.28423e+06 |          73.27 |           2279 |            2.14 | False          |
|   2010 |      10 | MN            | MRO           | East North Central | cold               |            -1.5 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |              3000 | severe weather     | heavy wind              |              nan |                70000 |          8.15 |   5.22212e+06 |          73.27 |           2279 |            2.14 | False          |
|   2012 |       6 | MN            | MRO           | East North Central | normal             |            -0.1 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |              2550 | severe weather     | thunderstorm            |              nan |                68200 |          9.19 |   5.78706e+06 |          73.27 |           2279 |            2.14 | False          |
|   2015 |       7 | MN            | MRO           | East North Central | warm               |             1.2 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |              1740 | severe weather     | nan                     |              250 |               250000 |         10.43 |   5.97034e+06 |          73.27 |           2279 |            2.14 | False          |

​
#### Univariate Analysis 
For our univariate analysis, we plotted the distribution for each in the cleaned dataset. One of the plots we found most interesting was the distribution of cause categories, as pictured below:

<iframe src="assets/fig1.univar_barplot.html"  width="1050" height="450"  frameborder="0"></iframe>


As we can see in the graph above, most of the outages are caused by severe weather and intentional attacks.

We also explored a couple more plots for our univariate analysis, but one of utmost interest to us was to pictographically visualize average power outages across the United States, which we did through a geomap (pictured below). We used median power outages to get a general understanding of the distribution across states in the USA.

<iframe src="assets/univar_choropleth.html"  width="1050" height="450"  frameborder="0"></iframe>
We see that states on the westcoast have significantly higher median power outage duration compared to east coast in the United States, which poses an interesting question of why this could be taking place.

#### Bivariate Analysis

For our bivariate analysis, we used a box plot to explore the differences in outage duration caused be different categories. Our choice of picking was between severe weather and intentional attacks, which we have pictured below:

<iframe src="assets/fig2.bivar_boxplot.html"  width="1000" height="450" frameborder="0" ></iframe>

We see that severe weather has a higher mean and a greater spread of durations, while intentional attacks tend to have shorter durations and fewer outliers. This can later be tested in our hypothesis test on whether or not they originate from the same distribution.


### Interesting Aggregates
The following pivot table shows the **mean outage duration** for each cause category in each climate region.

|    | CLIMATE.REGION     |   equipment failure |   fuel supply emergency |   intentional attack |   islanding |   public appeal |   severe weather |   system operability disruption |
|---:|:-------------------|--------------------:|------------------------:|---------------------:|------------:|----------------:|-----------------:|--------------------------------:|
|  0 | Central            |             322     |                 10035.2 |              490.25  |    125.333  |         1410    |          3299.63 |                        2695.2   |
|  1 | East North Central |           26435.3   |                 33971.2 |             2501.11  |      1      |          733    |          4434.82 |                        2610     |
|  2 | Northeast          |             269.75  |                 14629.6 |              264.68  |    881      |         2655    |          4429.9  |                         773.5   |
|  3 | Northwest          |             702     |                     1   |              488.831 |     73.3333 |          898    |          4838    |                         141     |
|  4 | South              |             295.778 |                 17482.5 |              337.667 |    493.5    |         1163.98 |          4391.35 |                         899.385 |
|  5 | Southeast          |             554.5   |                   nan   |              504.667 |    nan      |         2865.4  |          2685.71 |                         180.6   |
|  6 | Southwest          |             113.8   |                    76   |              274.678 |      2      |         2275    |         11572.9  |                         370.375 |
|  7 | West               |             524.81  |                  6154.6 |              886.267 |    214.857  |         2028.11 |          2928.37 |                         363.667 |
|  8 | West North Central |              61     |                   nan   |               47     |     68.2    |          439.5  |          2442.5  |                         nan     |

An interesting observation is that the East North Central region has significantly higher observations than other regions. This result is intersting to perform a permutation test on it.

# Assessment of Missingness 

### NMAR Analysis 
As per our analysis of the columns in this dataset, we observed that the column CAUSE.CATEGORY.DETAILS is potentially displaying NMAR. There are several inconsistencies in the data entry for this column, which make it appear as though it was manually entered by the researchers. For example, there are several variations of CAUSE.CATEGORY.DETAILS containing similar words such as: 
- 'heavy wind', 'wind storm', 'wind', 'wind/rain' 
- 'snow/ice ', 'snow/ice storm' 

which are variations of the same cause category. 

Another example would be errors in the spacing of entries. For example, 'Hydro' and ' Hydro' are both unique entries in the column even though it is essentially the same cause category.

Here is a list of the variables found in CAUSE.CATEGORY.DETAIL:

 [nan, 'vandalism', 'heavy wind', 'thunderstorm', 'winter storm', 'tornadoes', 'sabotage', 'hailstorm', 'uncontrolled loss', 'winter', 'wind storm', 'computer hardware', 'public appeal', 'storm', ' Coal', ' Natural Gas', 'hurricanes', 'wind/rain', 'snow/ice storm', 'snow/ice ', 'transmission interruption', 'flooding', 'transformer outage', 'generator trip', 'relaying malfunction', 'transmission trip', 'lightning', 'switching', 'shed load', 'line fault', 'breaker trip', 'wildfire', ' Hydro', 'majorsystem interruption', 'voltage reduction', 'transmission', 'Coal', 'substation', 'heatwave', 'distribution interruption', 'wind', 'suspicious activity', 'feeder shutdown', '100 MW loadshed', 'plant trip', 'fog', 'Hydro', 'earthquake', 'HVSubstation interruption', 'cables', 'Petroleum', 'thunderstorm; islanding', 'failure']



### Missingness Dependency

For our process of selecting which columns to explore missingness dependencies, we genereated a heatmap to visualize its proportion of missing values:

<iframe src="assets/fig4_missingness_heatmap.html" width="1000" height="450" frameborder="0" ></iframe>

From this heatmap, we see that DEMAND.LOSS.MW and CUSTOMERS.AFFECTED have a large proportion of missing data, while there is none in CAUSE.CATEGORY. Therefore, We decided to explore the missingness dependency of **CUSTOMERS.AFFECTED** on **CAUSE.CATEGORY**. We performed a **permutation test** to answer this question, and used **total variation distance (TVD)** as our test statistic of choice.

In summary:
**Test Statistic:** total variation distance

**Significance Level:** 0.05

**Observed Test Statistic:** 0.7557790341210083

The following histogram shows the observed distribution of **CAUSE.CATEGORY** separated by the missingess of the respective number of customers affected. 

<iframe src="assets/testplot.missingness_analysis.html" width="1000" height="450" frameborder="0" ></iframe>

This is the observed distribution of permutation TVD's against our observed TVD. We see that our observed TVD (the red line) is situated to the right of main (blue) distribution, which indicates that our test generated a p-value of 0 (approximately).

This essentially implies that there is a **significant difference** in the distribution of customers affected and cause category. We can conclude that CUSTOMERS.AFFECTED is likely dependent on the values of CAUSE.CATEGORY, making it **MAR dependent**. 

<iframe src="assets/fig5a.tvd.html" width="1000" height="450" frameborder="0" ></iframe>


# Hypothesis Testing

From our EDA, we observed that severe weather and intentional attack had the higest proportion of all cause categories, yet their mean outage duration differs signifcantly. As such, we will do a **permutation test** to determine whether or not they originate from the same distribution and the observed difference is due to random chance.

**Null Hypothesis:** The outage duration caused by severe weather and the outage duration caused by intentional attacks originate from the same distribution.

**Alternative Hypothesis:** The outage duration caused by severe weather and the outage duration caused by intentional attacks **do not** originate from the same distribution.

**Population:** The total set of outage durations across all categories and events present in the original dataset. 

**Sample size:** Subset of outage durations caused by severe weather and intentional attacks

<iframe src="assets/fig6.hypothesis_test.html" width="1000" height="450" frameborder="0"></iframe>

To determine our test statistic, we plotted the distribution of outage duration for each labels. Here, we see observe that the distributions have similar shapes, leading us to choose absolute difference in means as our test statistic.

**Test Statistic:** Absolute difference in means 

**Observed Test statistic:** 3377.776116612198

**Significance Level:** 0.05

**P-Value:** 0.0

<iframe
  src="assets/fig7.ht_result.html"
  width="1000"
  height="450"
  frameborder="0"
></iframe>

This plot shows us that there is a significant difference between the 2 cause categories, since our observed value is towards the far right of the plot.

**Conclusion:** Since the P-value was 0.0 (< 0.05 significance level), we reject our null hypothesis that outage durations caused by severe weather and outage duration caused by intentional attacks originate from the same distribution. This favours our alternative hypothesis, that there is in fact the two distributions originate from different distributions.


# Framing the Prediction Model

Following our investigation on the outage duration in relation to the cause of the power outage as well as the region in iwhich it occured, we see that there is a significant effect on outage duration by the outage being caused by severe weather. 

Looking at it further, we can look at the mean outage duration for each cause category:

| CAUSE.CATEGORY                |   OUTAGE.DURATION |
|:------------------------------|------------------:|
| equipment failure             |             224   |
| fuel supply emergency         |            3960   |
| intentional attack            |              92.5 |
| islanding                     |              77.5 |
| public appeal                 |             455   |
| severe weather                |            2464   |
| system operability disruption |             222   |


We can also observe the proportion of cause categories. 

| CAUSE.CATEGORY                |   OUTAGE.DURATION |
|:------------------------------|------------------:|
| equipment failure             |         0.0386266 |
| fuel supply emergency         |         0.0271817 |
| intentional attack            |         0.237482  |
| islanding                     |         0.0314735 |
| public appeal                 |         0.0493562 |
| severe weather                |         0.530043  |
| system operability disruption |         0.0858369 |

We see that the outage duration varies significantly for severe weather and fuel supply emergency. However, fuel supply emergency is not significant in terms of its proportion in the outage causes, while severe weather is. Therefore, we are going to do a **binary classification model on predicting whether or not a power outage is caused by 'severe weather'**. This can help utility companies and emergency responders better prepare for and manage power outages by identifying potential weather-related risks in advance and allocating resources more effectively.

We will use **F1 score** as our metric as the distribution of cause cateogry is not very balanced. Using F1 Score will help us account for this imbalance as it accounts for recall and precision.

# Baseline Model

First, we decided to implement a classification model using Logistic Regression based on the following variables to predict whether or not an outage is caused by severe weather:

- Climate Region (Nominal): This will help us account for any geographic significance for any severe weather-related power outages.  
- Month (ordinal): Weather may be more or less favorable/severe in certain periods
- Outage Duration (Quantitative): Severe weather related power outages may have correlatoin with outage duration.

Here, we one-hot encode the climate region and month while we kept outage duration as is without any processing.

### Results from our LogisticRegression:

```
f1 score on training data: 0.7391941509470169
f1 score on test data: 0.7237204323380247
Accuracy on training data: 0.7116095152603232
Accuracy on test data: 0.6944336917562725
```
Our baseline model already shows pretty good result for not tuning any hyperparameters and only using 3 features.

# Final Model

In our final model, we included the following features:
- Climate Region (Nominal): This will help us account for any geographic significance for any severe weather-related power outages.  
- Month (Ordinal): Weather may be more or less favorable/severe in certain periods
- Outage Duration (Quantitative): Severe weather related power outages may have correlatoin with outage duration.
- Outage Start (Ordinal): The start time of the outage can indiciate if an outage occured on the weekday or weekend. This may have some correlations with whether or not an outage is caused by severe weather. 
- Climate Category (Nominal): This encodes geographical and climate information and may indicate if a region is more susceptible to severe weather
- Total Sales (Quantitative): This may indicate if a region's energy infrastructure is strained due to excessive use.

The categorical features, climate region, climate category and months are one-hot encoded. The Outage start feature will be binary transformed through a custom transformer to determine if the outage occured on a weekday or weekend. The quantitative features (Total Sales and Outage Duration) is standardised through a transformer.

We also tested using different classifiers (logistic regression, a decision tree classifier, and a random forest classifier) to determine the best model for this task. It is important to note that for initial test runs, we performed the classification without implemnting a grid search to get a rough idea of which classifier to use. We did run 1000 iterations on different splits of the data and the results below are averaged:

### Logistic Regression:
```
f1 score on training data: 0.7601331977301075
f1 score on test data: 0.74431015253997
Accuracy on training data: 0.7404148550724637
Accuracy on test data: 0.7229494584837545
```

### Decision Tree Classifier:
```
f1 score on training data: 0.8044828429651232
f1 score on test data: 0.7865718074276548
Accuracy on training data: 0.7912880434782608
Accuracy on test data: 0.7716245487364622
```

### Random Forest Classifier:

```
f1 score on training data: 0.8328073100879739
f1 score on test data: 0.8060692996285136
Accuracy on training data: 0.8205634057971014
Accuracy on test data: 0.7917942238267148
```

We can see that the RandomForest performs the best of all the classifiers, in terms of both f1 score and accuracy on test data. 

#### Finding the best hyperparamters:

In order to find the best combination of hyperparameters to yield the best results, we used GridSearchCV to perform k-fold cross validation on our test data.

### Results from GridSearchCV:

```
 'classifer__criterion': 'entropy',
 'classifer__max_depth': 15,
 'classifer__n_estimators': 15
```

<iframe src="assets/grid_data.html" width="1000"  height="450"  frameborder="0"></iframe>
This graph above shows the f1-score performance depending on the hyperparameters.

Using these hyperparamaters, We were able to receive very good performacne for both the train and test data. We have an almost perfect f1-score on our train data, and a 85% f1 score for our test data. This is a significant increase in performance from our baseline model.
#### Training data:
```py
grids.score(X_train, y_train)
0.9798657718120805
```
#### Testing data:
```py
grids.score(X_test, y_test)
0.8409893992932863
```

# Fairness Analysis

For our fairness evaluation, we decided to assess if the model performs differently based on the season.

**Null Hypothesis**: The model is fair; the absolute difference in F1 scores between winter and summer months is due to random chance. This implies that any observed performance difference between the two groups is not significant.

**Alternative Hypothesis**: The model is unfair; the absolute difference in F1 scores between winter and summer months is significant and not due to random chance. This suggests that the model performs differently for winter and summer months in a way that is unlikely to be due to randomness.

#### Choice of Groups
    Group X: Winter months (December, January, February)
    Group Y: Summer months (June, July, August)

#### Evaluation Metric
    Metric: F1 Score

#### Choice of Test Statistic
    Test Statistic: Absolute difference in F1 scores between the groups.

#### Significance Level
    α = 0.05

#### Permutation Test Results
    Observed F1 score difference: 0.022343821249430018
    P-value: 0.701

<iframe src="assets/fig9.fairness_eval.html" width="1050"  height="450"  frameborder="0"></iframe>

#### Conclusion
Our chosen significance level is 0.05, and since our p-value > 0.05, we concluded that there is no significant difference in F1 scores between winter and summer months. Hence we fail to reject our null hypothesis, and our models' performance is fair with respect to seasonal differences. 








