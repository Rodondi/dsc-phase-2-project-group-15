# Real Estate Success Blueprint: Insights into Seasonal Sales and Property Features

### Table of Contents

* Project Overview
* Business Problem
* Data Understanding
* Data Cleaning and Preparation
* Exploratory Data Analysis
* Feature Engineering
* Feature Selection
* Modelling
* Challenges
* Improvements
* Business Recommendations

## Project Overview

In the ever-evolving world of real estate, making informed decisions is paramount to success. As an incoming real estate manager, understanding the dynamics of the market can be the key to unlocking your potential.

This project analyzes the King County House Sales dataset to understand how various factors affect property prices and make data-driven recommendations for real estate business strategies. The analysis includes cleaning the dataset, conducting exploratory data analysis (EDA), creating new features, building predictive models, and providing business insights.

Specifically, we delve into two crucial aspects:

1. **Seasonal Sales:** When is the optimal time to list your property for sale? We've dissected historical sales data to uncover trends and patterns, helping you pinpoint the best seasons for listing your properties.

2. **Property Features:** What property features should you consider when deciding what to put on your listing? Our analysis includes predictive models that take these features into account, assisting you in making more informed pricing decisions.


## Business Problem

In the dynamic realm of real estate, where property values fluctuate, market demand varies, and buyer preferences evolve, it's crucial to have a deep understanding of the industry's intricacies. Our project aims to address fundamental 2 business questions that can significantly impact your success in the field.

1. Explore the impact of seasons on property sales within the real estate market and quantify these effects.
2. Evaluate how property features affect property prices.

## Data Understanding

This project utilizes the King County House Sales dataset, which can be found in the `kc_house_data.csv` file in the `data` folder within this project's GitHub repository. The dataset provides a wealth of information related to real estate transactions in King County, Washington. Here's an overview of the key columns and their descriptions:

- **id:** A unique identifier for each house.
- **date:** The date when the house was sold.
- **price:** The sale price of the property (our prediction target).
- **bedrooms:** The number of bedrooms in the house.
- **bathrooms:** The number of bathrooms in the house.
- **sqft_living:** The square footage of the living space in the home.
- **sqft_lot:** The square footage of the lot.
- **floors:** The number of floors (levels) in the house.
- **waterfront:** A binary indicator of whether the house is on a waterfront (e.g., river, lake).
- **view:** A rating of the quality of the view from the house.
- **condition:** An assessment of the overall condition of the house, related to its maintenance.
- **grade:** An overall grade of the house, related to its construction and design.
- **sqft_above:** The square footage of the house apart from the basement.
- **sqft_basement:** The square footage of the basement.
- **yr_built:** The year when the house was originally built.
- **yr_renovated:** The year when the house was renovated.
- **zipcode:** The ZIP Code used by the United States Postal Service.
- **lat:** The latitude coordinate of the house's location.
- **long:** The longitude coordinate of the house's location.
- **sqft_living15:** The square footage of interior housing living space for the nearest 15 neighbors.
- **sqft_lot15:** The square footage of the land lots of the nearest 15 neighbors.

## Data Cleaning and Preparation

Before conducting any analysis or building predictive models, it's crucial to ensure the dataset is clean and free from inconsistencies. In this project, we performed the following data cleaning and preparation steps:

1. **Handling Missing Data:** We carefully identified columns with missing values and decided on appropriate strategies to address them. Depending on the nature and significance of missing data, we either imputed missing values or, in some cases, removed rows or columns with excessive missing data. This ensures that our analysis is based on as complete a dataset as possible.

2. **Dealing with Outliers:** Outliers can significantly impact model performance and distort insights. We employed robust techniques to detect and handle outliers in numerical features, such as the sale price, square footage, and more. This step helps in creating more robust and reliable predictive models.

3. **Addressing Data Integrity:** We verified data integrity by checking for inconsistencies and errors in the dataset. This involved examining data types, unique identifiers, and ensuring that categorical variables contain valid categories.

4. **Encoding Categorical Variables:** Many machine learning algorithms require numerical inputs. We encoded categorical variables using techniques like one-hot encoding or label encoding to ensure compatibility with these models.

## Exploratory Data Analysis

### Checking Statistical Details

We initiated our analysis by examining the statistical details of the numerical columns using the `df.describe()` function. This summary provided us with insights into the dataset's central tendencies, spreads, and potential outliers. Some notable statistics include:

- **Price**: The mean sale price is approximately $540,297, with a wide range of values, ranging from $78,000 to $7,700,000.

- **Bedrooms**: The dataset contains a wide distribution of bedroom counts, with a maximum of 33. There were outliers in this column, which we addressed.

- **Square Footage**: Various square footage metrics (e.g., living space, lot size) exhibit diverse ranges.

### Handling Outliers

We identified outliers in the `bedrooms` column with entries exceeding 20 bedrooms. These were replaced with the median value to ensure data integrity and prevent undue influence on our analyses.

## Feature Engineering

#### Feature 1: Sales vs. Seasons

We introduced a new feature, `season`, to capture the season in which a property was sold. This involved extracting the month from the `date` column and mapping it to the corresponding season (Spring, Summer, Autumn, or Winter). Analyzing sales patterns by season revealed valuable insights.

![image](https://github.com/Rodondi/dsc-phase-2-project-group-15/assets/133044105/b8591713-f8e2-4e5f-a67c-51d704fc3091)

*Average Selling Price Vs Season: This plot illustrates the average selling price across different seasons, highlighting seasonal variations in property sales.*

**Business Problem 1 Explanation**: The analysis indicates that Summer has the highest average sales, potentially due to favorable warm weather for property hunting. In contrast, Winter experiences the lowest number of sales. Stakeholders may consider adjusting their marketing and pricing strategies based on these seasonal patterns, focusing marketing efforts during Spring and Summer to maximize high property sales.

#### Feature 2: Age

We calculated the age of each property by subtracting the year built (`yr_built`) from the year of sale. This feature, `age`, provides insights into property age and its potential impact on prices.

#### Feature 3: Renovation

A binary feature, `renovated`, was created to indicate whether a property underwent renovation based on the `yr_renovated` column.

These feature engineering steps set the stage for more advanced analyses and predictive modeling, as we delve deeper into understanding the factors affecting property prices in King County.

## Feature Selection
 
### Defining Features and Target Variable

To begin, we defined our features (independent variables) and the target variable (the variable we aim to predict). The target variable, `price`, represents the sale price of properties. We constructed our feature matrix, `X`, by excluding the `price` and `date` columns, as the latter is non-numeric and does not directly contribute to our predictive model. The target variable, `y`, was set as the `price`.

### Data Splitting

To assess our model's performance, we divided the data into training and test sets. This splitting was achieved using the `train_test_split` function, with 80% of the data allocated to training and 20% for testing. A random seed (`random_state`) of 42 was utilized for reproducibility.

### Correlation Analysis

We employed correlation analysis to measure the strength of the relationship between each feature and the target variable, `price`. The correlation coefficient quantifies this relationship, with values closer to 1 indicating a strong positive correlation and values closer to -1 indicating a strong negative correlation. Features with correlations close to 0 are considered weakly correlated with the target variable.

Here are some key findings from the correlation analysis:

- **Strong Positive Correlations**: Features such as `sqft_living`, `grade`, `sqft_above`, and `sqft_living15` exhibit strong positive correlations with the `price`. These features are likely to have a significant impact on property prices.

- **Moderate Positive Correlations**: Features like `bathrooms`, `sqft_basement`, and `bedrooms` also positively correlate with `price`, although to a slightly lesser extent.

- **Weak Correlations**: Some features, such as `zipcode`, `age`, and `season`, display weak correlations with `price`, indicating a less pronounced relationship.

- **Negative Correlations**: While most features have positive correlations, there are no strong negative correlations, suggesting that none of the features have an overwhelmingly negative impact on property prices.

### Visualizing Correlations

A correlation heatmap was created to visually represent the correlations between numerical features. This heatmap provides a clear overview of the relationships between features and can help identify multicollinearity, where two or more features are highly correlated with each other.

![image](https://github.com/Rodondi/dsc-phase-2-project-group-15/assets/133044105/90259749-7a89-44e2-a06c-09dfe1f05a52)

*Correlation Heatmap Excluding 'date' and 'id': This heatmap visually presents the correlations between numerical features, offering insights into feature relationships and potential multicollinearity.*

## Modelling

### Creating a Baseline Model

We established a baseline model to benchmark our future models' performance. We utilized the `DummyRegressor` from scikit-learn, which predicts property prices without considering any features. This baseline model helped us gauge the effectiveness of more advanced models.

#### Baseline Model Results

- **R-squared**: 0.0
- **Mean Squared Error (MSE)**: 368,958.05
- **Mean Absolute Error (MAE)**: 235,058.25

### Model 1: Using Key Property Features

For our first predictive model, we selected a subset of features based on their strong positive correlations with the target variable (`price`) and their representation of essential property characteristics. The features include 'bedrooms', 'bathrooms', 'sqft_living', 'sqft_lot', and 'floors'.

#### Model 1 Results

- **Mean RMSE**: 257,825.19
- **Standard Deviation of RMSE**: 17,760.72

### Model 2: Adding Grade and Condition Features

In our second model, we expanded the feature set to include 'grade' and 'condition.' These features assess the overall quality, construction, and maintenance of properties, which can significantly influence property prices.

#### Model 2 Results

- **Mean RMSE**: 244,080.75
- **Standard Deviation of RMSE**: 19,250.64

### Model 3: Incorporating Renovation Status

Our third model introduced the 'renovated' feature to the set. This feature indicates whether a property has undergone renovation. Renovations can impact a property's overall condition and, consequently, its pricing.

#### Model 3 Results

- **Mean RMSE**: 241,808.57
- **Standard Deviation of RMSE**: 18,716.30

### Model 4

We created Model 4 to assess the impact of removing features that led to a price decrease. 
We aimed to understand how the exclusion of certain variables affects predictions.

#### Model 4 Results
- **Mean RMSE**: 242,115.34
- **Standard Deviation of RMSE**: 18,736.49

### Model Comparison and Selection

Among the models, Model 3 stands out as the best performer, achieving an average RMSE of approximately 241,808.57. This indicates that, on average, our predictions deviate from actual property values by approximately $241,808.57.

Our models offer valuable insights into property price prediction, enabling better decision-making in the real estate market. By considering the features identified in Model 3, you can make more accurate price predictions and optimize your real estate strategies.

Additionally, we tested Model 3 on unseen data, and its performance remains consistent with an RMSE of approximately 242,102.21 and a low standard deviation of 11,348.26. This signifies that Model 3 is reliable and performs consistently across different subsets of data.

For further improvements and exploration, consider fine-tuning models, addressing multicollinearity issues, or incorporating additional features and data sources to enhance prediction accuracy.

## Business Recommendations

### 1. **Strategic Listing Timing and Seasonal Analysis**

* **Recommendation**: Use the insights gained from seasonal sales patterns to strategically time property listings. Aim to list properties during high-demand seasons, such as Spring and Summer, when buyers are more active.

* **Impact**: By listing your properties at the right time, you can potentially attract more buyers, create a sense of urgency, and optimize your chances of achieving higher sale prices.

### 2. **Property Feature Emphasis**

* **Recommendation**: Pay close attention to property features that have a strong positive impact on prices, such as square footage, the number of bedrooms and bathrooms, and overall condition.

* **Impact**: Highlight these desirable features in your property listings and marketing materials to attract potential buyers. Accurate feature-based pricing can also make your listings more competitive in the market.

### 3. **Location and Neighborhood Analysis**

* **Recommendation**: Explore the impact of location and neighborhood on property values. Consider factors like proximity to city centers, schools, public transportation, and safety.

* **Impact**: Understanding how location influences prices can help you make informed decisions about property investments and guide buyers in their search for the ideal neighborhood.

### 4. **Property Renovation Strategy**

* **Recommendation**: Assess the potential return on investment (ROI) for property renovations. Utilize data on renovated properties to make informed decisions about when and how to renovate.

* **Impact**: Renovations that align with market demand can increase property values and attract buyers willing to pay a premium for modernized homes.

### 5. **Market Segmentation**

* **Recommendation**: Implement market segmentation strategies to tailor your marketing efforts and property listings to different buyer segments. Consider factors like budget, preferences, and lifestyle.

* **Impact**: Personalized marketing and property recommendations can lead to more successful sales and satisfied clients.

### 6. **Market Trends and Adaptability**

* **Recommendation**: Stay updated with market trends, regulations, and technological advancements in the real estate industry. Be adaptable and prepared to adjust your strategies as the market evolves.

* **Impact**: Being informed and adaptable positions you to capitalize on emerging opportunities and navigate challenges effectively.

### 7. **Collaborate with Real Estate Industry Experts**

* **Recommendation**: Collaborate with real estate professionals and market experts who possess in-depth knowledge and experience in the industry. Leverage their insights to complement data-driven analyses.

* **Impact**: Expert collaborations can provide valuable perspectives, enhance decision-making, and foster industry connections.

### 8. **Exploring Additional Data Sources**

* **Recommendation**: Explore additional data sources that can offer deeper insights into market trends, customer behavior, and competitor activities.

* **Impact**: Expanding your data sources can enrich your analyses and provide a more comprehensive view of the real estate landscape.

### 9. **Competitor Price Monitoring**

* **Recommendation**: Continuously monitor and analyze competitors' pricing strategies to maintain competitiveness and optimize revenue.

* **Impact**: Staying ahead of the competition ensures that your properties remain attractive to potential buyers and sellers.

### 10. **Customer Feedback and Insights**

* **Recommendation**: Gather feedback from customers, including buyers and sellers, to better understand their preferences and experiences.

* **Impact**: Customer insights can guide your strategies, improve customer satisfaction, and refine the services you offer.

## Next Steps

As with any data-driven project, there are opportunities for further enhancements and refinements to increase its value and effectiveness. Some key areas for improvement include:

### 1. Data Enrichment

Expanding the dataset to include additional relevant variables, such as neighborhood crime rates, school quality, and proximity to amenities, can provide a more comprehensive view of property values. Enriching the data with external sources can lead to more accurate predictions.

### 2. Geographic Analysis

Incorporating geospatial data analysis can provide deeper insights. Analyzing the influence of location, such as proximity to city centers, public transportation, or green spaces, can offer valuable information for both buyers and sellers.

### 3. Real-time Data Updates

Consider implementing a mechanism to update the dataset with real-time market data. This feature would allow users to access the most current insights and adapt their strategies accordingly.

### 4. Market Segmentation

**Enhancement**: Implement segmentation analysis to identify distinct market segments based on buyer preferences. Tailor recommendations and strategies for different segments to maximize their effectiveness.

---
