# 🏨 Unveiling Hotel Performance: An In-Depth Analysis of Reservation Cancellations
<br>

**Platform**: Jupyter Notebook | [Notebook via nbviewer](https://nbviewer.org/github/buddymar/Hotel-Reservation-Cancellation/blob/main/Hotel%20Reservation%20Cancellation.ipynb) | [Notebook via Github](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/Hotel%20Reservation%20Cancellation.ipynb)<br>
**Programming Language**: Python <br>
**Libraries**: Pandas, NumPy, Matplotlib, Seaborn <br>
**Database**: MySQL <br>
**Dashboard**: Tableau | [View Dashboard](https://public.tableau.com/views/HotelReservationandCancelation/Dashboard1?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link)<br>
**Source Data**: Kaggle <br>
<br>

**Table of Contents**
- [Introduction](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#-introduction)
- [Source Data](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#-data-scraping)
- [Data Integration](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#-data-integration)
- [Data Preprocessing](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#-data-preprocessing)
	- [Data Cleaning](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#-data-preprocessing)
      - [Missing Values](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#missing-values)
      - [Data Anomaly](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#duplicated-values)
- [Exploratory Data Analysis](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#-exploratory-data-analysis)
  - [Hotel Performance Metrics](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#player-attributes)
      - [Total Booking per Hotel Type](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#missing-values)
      - [Booking per Month](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#missing-values)
      - [ADR per Month](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#missing-values)
  - [Reservation Cancellation](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#player-basic-stats)
      - [Cancellation per Month](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#missing-values)
      - [Cancellation per Stay Duration](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#missing-values)
      - [Cancellation per Lead Time](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#missing-values)
      - [Cancellation per Distribution Channel](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#missing-values)
      - [Travel Agent/Tour Operator](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#missing-values)
- [Conclusion & Business Insight](https://github.com/buddymar/NBA-MVP-Predictions/blob/main/README.md#-predictive-modeling)
<br>

---

## 📌 **Introduction**

<p align="center">
    <kbd> <img width="1000" alt="mvp banner" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/hotel2.bmp"> </kbd> <br>
</p>

The hospitality industry, particularly in destinations like Denpasar, Indonesia, where both City Hotels and Resort Hotels flourish, presents a dynamic landscape for analysis. In this comprehensive analysis, we delve into a meticulous examination of hotel performance and reservation cancellation patterns within these two distinct hotel categories.

Our analysis embarks on a journey to unravel the intricate dynamics of hotel performance and reservation cancellations, shedding light on critical facets that influence operational efficacy and guest satisfaction. Through meticulous data examination, we aim to discern the underlying trends, challenges, and opportunities inherent in the operations of these hotel types, fostering actionable insights for stakeholders within the hospitality industry. In this report, we will focus on:

**Hotel Performance Analysis:**
- Exploration of booking composition, providing insights into the distribution of reservations between City Hotels and Resort Hotels.
- Examination of monthly booking patterns and Average Daily Rate (ADR) fluctuations to discern seasonal trends and pricing dynamics.
- Evaluation of key performance metrics to gauge the operational efficiency and revenue-generating capabilities of each hotel type.

**Reservation Cancellation Investigation:**
- In-depth analysis of factors contributing to reservation cancellations, including guest behavior, external influences, and operational inefficiencies.
- Identification of critical aspects impacting cancellation rates and their implications for revenue management and guest satisfaction.
- Formulation of actionable strategies and recommendations to mitigate reservation cancellations and optimize hotel revenue streams.

By dissecting the nuances of hotel performance and reservation dynamics, this analysis endeavors to equip industry stakeholders with actionable insights to enhance operational efficiency, maximize revenue potential, and elevate the guest experience in Denpasar's diverse hospitality landscape.

<br>

## 📌 **Source Data**

For this analysis, the data stored in MySQL databases will be utilized. The data, records, and information required for the analysis will be extracted from `hotel_notebook` database using SQL queries.

<p align="center">
    <kbd> <img width="1000" alt="bref" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/Database%20Diagram.png"> </kbd> <br>
</p>

<br>

## 📌 **Data Integration**

We will use SQL joins to create a new dataset by incorporating new data from all other tables into the `hotel_dataset` table.

<p align="center">
    <kbd> <img width="1000" alt="bref" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/joins.png"> </kbd> <br>
</p>

<br>

## 📌 **Data Preprocessing**

### Missing Values

Before begin the analysis, we need to ensure that all missing values are addressed. We'll start by identifying all features with missing values and then handle them using the most appropriate method.

Table 1 — Missing Values
 **Column** | **Total Missing Values** | **Handling Missing Values**
-----------------|--------------|--------------|
company | 112593 | The missing values in the `company` feature will be filled with **0**, as these values indicate that the distribution channel for this particular guest is not a company.
agent | 16340 | The missing values in the `agent` feature will also be filled with **0**, for the same reason as above.
city | 488 | For the `children` feature, missing values will be filled with **0**, as this indicates that the guest did not bring any children with them.
children | 4 | The missing values in the `city` feature will be filled with **unknown,** as there is no other method available to determine the guest's city of origin.

<br>

### Data Anomaly

In this section, we will filter out abnormal data from the dataset related to hotel reservations. This process ensures that the analysis relies on valid and reliable information.

### 1. Reservation Without Guests

<p align="center">
    <kbd> <img width="1000" alt="bref" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/anomaly1.png"> </kbd> <br>
</p>

### 2. Reservation With a Stay Duration of Zero Days

<p align="center">
    <kbd> <img width="1000" alt="bref" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/anomaly2.png"> </kbd> <br>
</p>

<br>

## 📌 **Exploratory Data Analysis**

The Exploratory Data Analysis (EDA) will focus on analyzing all available data and information related to winning the NBA MVP award. It will primarily be divided into:
- Player Attributes
- Player Basic Stats
- Player Advanced Stats
- Teams Performance

<br>

### Player Attributes

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/vote_share.png"> </kbd> <br>
</p>

<p align="center">
    <kbd> <img width="1000" alt="pos" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/position.png"> </kbd> <br>
</p>

**Key Points:**
- MPV winners consistently receive high vote shares, often close to or exceeding 90%, indicating strong support from NBA voters for their MVP candidacy.
- Despite the subjective nature of MVP voting, the consistently high vote shares for winners suggest a certain level of consensus among voters regarding the most deserving candidate. However, there may still be biases or factors influencing the voting process, such as media coverage, team success, or individual narratives.
- While power forwards and point guards have historically dominated MVP awards from 2001 to 2023, the last three MVP winners have been centers. Centers are traditionally known for their defensive presence, rebounding, and rim protection, but recent MVP-winning centers also excel offensively, showcasing versatility in their skill sets.

<br>

### Player Basic Stats

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/basic%20stats.png"> </kbd> <br>
</p>

**Key Points:**
- MVP winners exhibit superior performance across various statistical categories compared to both MVP vote-getters and all players.
- **Statistical excellence, particularly in scoring, shooting efficiency, playmaking, and defensive contributions, appears to be a common trait among MVP winners.**

<br>

### Player Advanced Stats

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/adv%20stats.png"> </kbd> <br>
</p>

<p align="center">
    <kbd> <img width="1000" alt="pos" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/bpm.png"> </kbd> <br>
</p>

**Key Points:**
- Advanced/analytical statistics provide a more nuanced understanding of player performance, focusing on efficiency, usage, and impact on both ends of the court.
- MVP winners consistently demonstrate superior performance across various advanced metrics compared to both MVP vote-getters and all players, emphasizing their overall impact and contribution to their teams' success.
- It's undeniable that OBPM can provide more insight into a player's value than DBPM. A player can receive MVP votes solely based on their offensive performance, even if they have little defensive impact while on the court. However, it's worth noting that many MVP winners also have high DBPM, which sets them apart from other vote-getters.

<br>

### Team Stats

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/team%20stats.png"> </kbd> <br>
</p>

<p align="center">
    <kbd> <img width="1000" alt="pos" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/team%20win%20vs%20win%20share.png"> </kbd> <br>
</p>

**Key Points:**
- Teams with MVP-caliber players tend to outperform their counterparts in terms of offensive and defensive efficiency, margin of victory, win-loss records, and overall and conference standings.
- Higher overall and conference standings among MVP-winning teams reflect their ability to elevate team performance and competitiveness, positioning them as key leaders in guiding their teams to success within their respective conferences and the league as a whole.

<br>

## 📌 **Predictive Modeling**

To predict the NBA MVP from this dataset, three models will be compared: Random Forest, XGBoost, and Extra Trees Regressor. The best-performing model will then be used for predicting and tracking the current season's NBA MVP. Given the imbalanced nature of the target variable, which often includes many zero values, the Root Mean Squared Logarithmic Error (RMSLE) will be used as the scoring metric.

<br>

### Modeling

Table 2 — Model Scoring
 **Model** | **RMSLE** | **R-squared** | **Best Hyperparameters** |
-----------------|--------------|--------------|--------------|
RandomForestRegressor | 0.2333 | 0.9063 | 'max_depth': 8, 'max_features': 'auto', 'min_samples_leaf': 3, 'min_samples_split': 6, 'n_estimators': 100
ExtraTreesRegressor | 0.2408 | 0.9087 | 'max_depth': 7, 'max_features': 'auto', 'min_samples_leaf': 3, 'min_samples_split': 6, 'n_estimators': 100
XGBRegressor | 0.155 | 0.9705 | 'colsample_bytree': 1.0, 'gamma': 0.1, 'learning_rate': 0.05, 'max_depth': 6, 'min_child_weight': 3, 'n_estimators': 63, 'reg_alpha': 0.5, 'reg_lambda': 1.0, 'subsample': 0.9
<br>

### Model Prediction

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/model%20prediction.png"> </kbd> <br>
</p>

**Key Points:**
- Based on the NBA MVP predictions for 2001-2023 winners, the XGBoost model had the best performance, achieving the highest accuracy with 22 correct predictions out of 23 winners. The Extra Trees model made 19 correct predictions, while the Random Forest model made 18 correct predictions.
- Interestingly, all three models incorrectly predicted the MVP for the 2017 season, selecting James Harden instead of Russell Westbrook.
- Moreover, all three models predict Nikola Jokić as the MVP for the current 2024 season (as of March), with a high predicted vote share.
- Overall, the models demonstrated high accuracy in predicting the NBA MVP, with XGBoost leading the pack with an accuracy ratio of 22 out of 23 (95.65%).

<br>

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/top3%20mvp.png"> </kbd> <br>
</p>

**Key Points (as of March 2024):**
- Nikola Jokić, with the highest PER, WS, and BPM, likely contributes significantly to the model predicting him as the number one of the top 10 MVP frontrunners.
- Shai Gilgeous-Alexander (2nd) and Giannis Antetokounmpo (3rd) still have a chance to move up in the MVP ranking ladder based on their actual basic stats, advanced stats, team standings, and vote share prediction.
- Luka Dončić leads in PTS per game (34.1) this season, with a considerable gap to the second highest, Shai Gilgeous-Alexander (30.9). This contributes to Dončić being in 4th place currently, despite his team's poor standings.

<br>

### Model Interpretation

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/shap%20value.png"> </kbd> <br>
</p>

The feature with the highest impact on the XGBoost model prediction is `adj_W%`, which represents the team's winning percentage adjusted by the total basic stats of the player. The impact gap from this feature to the next feature is considerable. Following closely are the next two impactful features for the model: `Total_AdvStat`, representing the total advanced stats for the player, and adjusted `BPM`, which indicates the Box Plus/Minus of the player.

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/NBA-MVP-Predictions/main/assets/shap%20bee.png"> </kbd> <br>
</p>

From the beeswarm plot, we can discern in greater detail the influence of each feature in this model. The plot vividly illustrates the wide range of impact from the `adj_W` feature. Additionally, it's apparent that features with high-value records exert the most influence on the model's predictions. Conversely, most low-value records result in zero impact across all features, except for `AST`, `Age`, and `Year`.
