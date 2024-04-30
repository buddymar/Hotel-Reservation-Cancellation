# 🏨 Unveiling Hotel Performance: An In-Depth Analysis of Reservation Cancellations
<br>

**Platform**: Jupyter Notebook | [View Notebook on nbviewer](https://nbviewer.org/github/buddymar/Hotel-Reservation-Cancellation/blob/main/Hotel%20Reservation%20Cancellation.ipynb) | [View Notebook on Github](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/Hotel%20Reservation%20Cancellation.ipynb)<br>
**Programming Language**: Python <br>
**Libraries**: Pandas, NumPy, Matplotlib, Seaborn <br>
**Database**: MySQL <br>
**Dashboard**: Tableau | [View Dashboard](https://public.tableau.com/views/HotelReservationandCancelation/Dashboard1?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link)<br>
**Source Data**: Kaggle <br>
<br>

**Table of Contents**
- [Introduction](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#-introduction)
- [Source Data](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#-source-data)
- [Data Integration](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#-data-integration)
- [Data Preprocessing](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#-data-preprocessing)
	- [Data Cleaning](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#-data-preprocessing)
      - [Missing Values](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#missing-values)
      - [Data Anomaly](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#data-anomaly)
- [Exploratory Data Analysis](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#data-anomaly)
  - [Hotel Performance Metrics](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#total-booking-per-hotel-type)
      - [Total Booking per Hotel Type](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#total-booking-per-hotel-type)
      - [Booking per Month](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#booking-per-month)
      - [ADR per Month](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#adr-per-month)
  - [Reservation Cancellation](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#cancellation-per-month)
      - [Cancellation per Month](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#cancellation-per-month)
      - [Cancellation per Stay Duration](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#cancellation-per-stay-duration)
      - [Cancellation per Lead Time](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#cancellation-per-lead-time)
      - [Cancellation per Distribution Channel](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#cancellation-per-distribution-channel)
      - [Travel Agent/Tour Operator](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#travel-agenttour-operator)
- [Conclusion & Business Insight](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#-conclusion--business-insight)
- [Dashboard](https://github.com/buddymar/Hotel-Reservation-Cancellation/blob/main/README.md#-dashboard)

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

The exploratory data analysis (EDA) will be divided into two main parts, each focusing on distinct aspects of the dataset:
- Hotel Performance
	- Total Booking per Hotel Type
   	- Booking per Month
   	- ADR per Month
- Hotel Reservation Cancellation
	- Cancellation per Month
   	- Cancellation per Stay Duration
   	- Cancellation per Lead Time
   	- Cancellation per Distribution Channel
   	- Travel Agent/Tour Operator

<br>

### Total Booking per Hotel Type

<p align="center">
    <kbd> <img width="500" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/hotelbookpct.png"> </kbd> <br>
</p>

**Key Points:**
- **City hotels** are more popular among guests, as they have a higher percentage of reservations compared to **resort hotels**.
- This could suggest that there is a higher demand for accommodations in urban areas compared to resort destinations.

<br>

### Booking per Month

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/bookpermonth.png"> </kbd> <br>
</p>

**Key Points:**
- **City hotels** always have **higher monthly booking** counts compared to **resort hotels**.
- Both types of hotels experience fluctuations in booking counts throughout the year, with peaks during holiday season for locals and summer months for tourists.
- **City hotels** see a notable increase in bookings during the holiday season / summer months, whereas **resort hotels** show more consistent booking counts throughout the year.

<br>

### ADR per Month

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/adrpermonth.png"> </kbd> <br>
</p>

**Key Points:**
- **City hotels** generally command **higher average daily rates (ADR)** compared to **resort hotels** across all months.
- Monthly ADR tends to peak during the holiday season for both **city and resort hotels**.

<br>

### Cancellation per Month

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/cancelpermonth.png"> </kbd> <br>
</p>

**Key Points:**
- **City Hotel** generally exhibits **higher cancellation rates** compared to **Resort Hotel** across all months.
- **City Hotel's** cancellation rates range from 37% to 47%, while **Resort Hotel's** cancellation rates range from 15% to 34%.
- Both hotel types experience fluctuations in cancellation rates throughout the year, with peak months typically occurring during the holiday season or summer season (June, July, August).

<br>

### Cancellation per Stay Duration

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/cancelstay.png"> </kbd> <br>
</p>

**Key Points:**
- Across both **City Hotel** and **Resort Hotel**, **shorter stay durations generally exhibit lower cancellation rates**.
- 1-day stays have the lowest cancellation rate.
- Both hotels show variability in cancellation rates across different stay durations.
- Longer stay durations, such as 2 weeks and onwards, tend to have higher cancellation rates compared to shorter durations.

<br>

### Cancellation per Lead Time

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/cancellead.png"> </kbd> <br>
</p>

**Key Points:**
- **City Hotel has a higher cancellation ratio compared to the Resort Hotel across all lead time groups**.
- As lead time increases, the percentage of cancellations generally increases for both hotel types. For instance, both hotels show significantly lower cancellation rates for reservations made 1 Day in advance compared to longer lead times.
- **Lead time plays a crucial role in reservation cancellations, with longer lead times correlating with higher cancellation rates.**

<br>

### Cancellation per Distribution Channel

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/canceldist.png"> </kbd> <br>
</p>

**Key Points:**
- **TA/TO (Travel Agent/Tour Operator) is the dominant distribution channel for both City Hotel and Resort Hotel**, with the highest number of reservations and cancellations for both.
- Direct bookings have the lowest cancellation rates for both hotels, with City Hotel at 18.36% and Resort Hotel at 17.03%.
- Both City Hotel and Resort Hotel should fostering a collaborative and communicative relationship with travel agents, so they can work together more effectively to minimize cancellations.

<br>

### Travel Agent/Tour Operator

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/agent1.png"> </kbd> <br>
</p>

**Key Points:**
- **The top 10 agents with the highest cancellation ratios at city hotels all have cancellation rates above 70%. Remarkably, the top 3 agents even exhibit a 100% cancellation rate**.
- **Agent 9 has the highest number of reservations (31849) and ranks first in terms of total reservations**. This agent seems to bring in a significant amount of business to the City Hotel. **However, Agent 9 also has a relatively high cancellation rate (41.62%)**, which might be a concern for the hotel's revenue management. Despite bringing in a large number of reservations, a high cancellation rate can lead to revenue loss and operational inefficiencies.
- Agents with lower rankings in terms of total reservations might still contribute positively to the hotel's revenue if they have lower cancellation rates. For example, **Agent 28 ranks sixth in terms of total reservations but has a relatively low cancellation rate (6.71%), indicating a more stable and reliable booking pattern**.
- Among the top 10 agents with the highest total reservations at city hotels, **agents 1 and 19** also rank in the top 10 agents with the highest cancellation rates.

<br>

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/agent2.png"> </kbd> <br>
</p>

**Key Points:**
- The top 10 agents with the highest cancellation ratios at city hotels all have cancellation rates in range 40% - 80%.
- **Agent 240 leads in total reservations with a substantial count of 13778, securing the top rank in this category.** This agent significantly contributes to the Resort Hotel's bookings. **Despite Agent 240's high volume of reservations, their cancellation rate is noteworthy**, indicating potential revenue volatility. Effective management strategies are necessary to mitigate revenue risks associated with high cancellation rates.
- Other agents, such as **Agent 250; 241; and 40, also exhibit substantial reservation counts but maintain relatively lower cancellation rates**. These agents represent opportunities for stable revenue streams with fewer cancellations.
- **Agents 240 and 96**, who are among the top 10 agents with the highest total reservations at resort hotels, also find themselves among the top 10 agents with the highest cancellation rates.

<br>

## 📌 **Conclusion & Business Insight**

In this comprehensive analysis of hotel performance and reservation dynamics in Denpasar, Indonesia, we have uncovered valuable insights that shed light on the intricacies of the hospitality industry. Here are the key takeaways from our findings:

---
1. `Demand Disparity between City and Resort Hotels:`
   - City hotels emerge as the preferred choice among guests, boasting higher reservation percentages and average daily rates (ADR) compared to resort hotels.
   - The higher demand for city accommodations underscores the need for resort hotels to refine their marketing strategies to attract more guests and increase their reservation percentages.
---  
2. `Seasonal Booking Trends and Revenue Optimization:`
   - Both city and resort hotels experience fluctuations in booking counts throughout the year, with peaks coinciding with holiday seasons for locals and summer months for tourists.
   - City hotels witness significant booking surges during peak seasons, while resort hotels maintain relatively consistent booking counts year-round.
   - Effective pricing and marketing strategies tailored to seasonal variations can help city hotels maintain consistent booking counts during off-peak months, while resort hotels can capitalize on peak seasons with attractive packages and promotions.
---
3. `Cancellation Rate Dynamics and Revenue Management:`
   - City hotels exhibit higher cancellation rates compared to resort hotels across all months and lead time groups.
   - Shorter stay durations generally correspond to lower cancellation rates for both hotel types, highlighting the importance of optimizing room allocation management.
   - Direct bookings demonstrate the lowest cancellation rates, emphasizing the need for hotels to incentivize guests to book directly through their channels to minimize revenue loss from cancellations.
---
4. `Impact of Distribution Channels on Cancellation Rates:`
   - Travel agents/tour operators (TA/TO) emerge as the dominant distribution channel for both city and resort hotels, accounting for the highest number of reservations and cancellations.
   - While TA/TO channels bring significant business, they also contribute to higher cancellation rates, necessitating collaborative efforts between hotels and agents to minimize cancellations and optimize revenue.
---
5. `Agent Performance Analysis and Revenue Risk Management:`
   - Certain agents exhibit exceptionally high cancellation rates, posing revenue volatility risks despite their substantial contribution to total reservations.
   - Effective revenue risk management strategies are crucial to mitigate the impact of high cancellation rates, particularly for agents with significant reservation volumes.
---
In conclusion, our analysis underscores the importance of understanding booking dynamics, cancellation patterns, and the role of distribution channels in optimizing revenue and enhancing guest satisfaction in the competitive hospitality landscape of Denpasar. By leveraging these insights, hotels can implement targeted strategies to maximize revenue potential, mitigate risks, and elevate the overall guest experience.

<br>

## 📌 **Dashboard**

[View Dashboard in Tableau Public](https://public.tableau.com/views/HotelReservationandCancelation/Dashboard1?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link)

To enhance our understanding and analysis of hotel performance and reservation cancellations, we can utilize this dashboard to highlight key performance indicators (KPIs) or metrics of interest. The dashboard comprises two pages: one focusing on hotel performance and the other on reservation cancellations. Each page provides an overview and detailed insights into the hotel data used in the notebook analysis.

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/dashboard1.png"> </kbd> <br>
</p>

<p align="center">
    <kbd> <img width="1000" alt="share" src="https://raw.githubusercontent.com/buddymar/Hotel-Reservation-Cancellation/main/assets/dashboard2.png"> </kbd> <br>
</p>
