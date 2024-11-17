Electric Vehicle Production and Its Impact on Climate: A Data Analysis Project
Overview
This project explores the impact of electric vehicle (EV) production on air pollution and CO2 emissions worldwide over the past 11 years. We analyzed data on electric vehicle production, CO2 emissions, oil displacement, and other related variables to understand whether the increased adoption of EVs has contributed to a reduction in global air pollution and climate change.

Research Question
Has the production of electric vehicles in the last 11 years affected the amount of air pollution throughout the world?

Hypothesis
We hypothesize that while the production of electric vehicles (EVs) has increased over the past 11 years, it has had a relatively small impact on reducing air pollution and CO2 emissions. This is due to the fact that gasoline-powered vehicles still dominate the global car fleet. Additionally, large industrial sources of pollution likely offset the contributions made by EVs in terms of improving air quality.

Dataset
The dataset used for this analysis contains global data on:

EV sales (BEV and PHEV)
Oil displacement (in million barrels per day)
CO2 emissions per vehicle produced (for both BEVs and PHEVs)
Total motor car production per year
The dataset spans the years from 2010 to 2021.

Methodology
We performed the following analyses to investigate the effect of EV production on air pollution and climate change:

Data Cleaning: We cleaned the dataset by removing irrelevant columns, correcting data types, and ensuring consistency in the values.
Correlation Analysis: We examined the relationship between electric vehicle sales and oil displacement using Pearson's correlation coefficient.
Regression Analysis: A multiple linear regression model was used to explore how EV sales and other factors (e.g., total vehicle production) contribute to oil displacement.
CO2 Emission Trends: We analyzed the trends in CO2 emissions per vehicle produced over time to understand the impact of EV production on global CO2 emissions.
Production Trends: We analyzed the growth of electric vehicle production compared to total motor vehicle production.
Key Findings:
Correlation Analysis: A strong correlation was found between EV sales and oil displacement, suggesting that as more EVs are produced, oil consumption decreases. However, correlation does not imply causation, and further research is needed to confirm this relationship.
Regression Analysis: The regression model suggested that while EV sales contribute to oil displacement, the overall effect on reducing oil consumption is not as significant as expected, possibly due to overfitting or the influence of other variables.
CO2 Emissions: The average CO2 emissions per BEV and PHEV decreased over time, indicating improvements in manufacturing processes.
EV Production Trends: From 2010 to 2021, the percentage of EVs sold globally increased from less than 1% to over 10%, signaling significant growth in EV adoption. However, gasoline-powered vehicles still dominate.
Project Code
The project was implemented using Python and the following libraries:

Pandas: For data manipulation and analysis.
NumPy: For numerical operations.
Matplotlib & Seaborn: For data visualization.
Statsmodels: For regression analysis.

Key Code Snippets:

Data Cleaning:

import pandas as pd
df = pd.read_csv("Electric_Cars_VS_Motor_Cars.csv", sep=';')
df = df.drop(columns=['EV Stock BEV', 'EV Stock PHEV', 'Electricity demand BEV', 'Electricity demand BHEV'])
df["Oil displacement (Million barrels per day)"] = df["Oil displacement (Million barrels per day)"].str.replace(",", ".")
df["Oil displacement (Million barrels per day)"] = df["Oil displacement (Million barrels per day)"].astype(float)

Correlation Analysis:

import seaborn as sns
import matplotlib.pyplot as plt
correlation_coefficient = df['EV sales BEV'].corr(df['Oil displacement (Million barrels per day)'])
sns.scatterplot(x='EV sales BEV', y='Oil displacement (Million barrels per day)', data=df)

Regression Analysis:

import statsmodels.api as sm
X = df[['EV sales BEV', 'EV sales PHEV', 'Total Motor cars production per year']]
y = df['Oil displacement (Million barrels per day)']
X = sm.add_constant(X)
model = sm.OLS(y, X).fit()

CO2 Emission Trends:

df['Avg CO2 BEV'] = df['Average CO2 emission per BEV produced (Kg CO2e)'] / df['EV sales BEV']
df['Avg CO2 PHEV'] = df['Average CO2 emission per PHEV produced (Kg CO2e)'] / df['EV sales PHEV']
plt.plot(df['Year'], df['Avg CO2 BEV'], label='BEV')
plt.plot(df['Year'], df['Avg CO2 PHEV'], label='PHEV')
plt.xlabel('Year')
plt.ylabel('Average CO2 Emission per Car (Kg CO2e)')
plt.title('Trends in Average CO2 Emissions per Car Produced')

Production Trends:

df2 = df[['Year', 'EV sales BEV', 'Total Motor cars production per year']]
df2['EV percentage'] = df2['EV sales BEV'] / df2['Total Motor cars production per year'] * 100
plt.plot(df2['Year'], df2['Total Motor cars production per year'], label='Total Motor Cars Production')
plt.plot(df2['Year'], df2['EV sales BEV'], label='EV Sales BEV')
plt.legend()
plt.xlabel('Year')
plt.ylabel('Number of Vehicles by 10s of Millions')
plt.title('EV Production vs. Total Vehicle Production')

Results and Conclusion
Based on our analysis, we conclude that while the production of electric vehicles has been increasing, its direct impact on reducing global air pollution and CO2 emissions has been limited. The global fleet is still dominated by gasoline-powered vehicles, and industrial pollution likely has a larger impact on climate change than the production of EVs alone.

Limitations:
Scope of Data: The dataset is global in scope, making it difficult to draw conclusions about specific regions or countries where EV adoption and environmental factors vary significantly.
Missing Variables: Key factors such as the energy mix used to charge EVs (renewable vs. non-renewable) and industrial pollution were not considered in the analysis, which could have influenced the results.
Overfitting: The regression model may have been overfitted, which could impact the reliability of the conclusions.
Future Work:
Regional Analysis: Focusing on specific regions could provide more targeted insights into the effectiveness of EVs in reducing emissions.
Energy Mix: Future analysis should incorporate the source of electricity used to charge EVs, as this has a significant impact on their overall carbon footprint.
Long-Term Trends: Additional years of data could help clarify longer-term trends in the impact of EV adoption on air pollution.

Installation Requirements
To run the project on your local machine, make sure you have the following Python libraries installed:

pip install pandas numpy seaborn matplotlib statsmodels

