**Customer Churn Analysis Dashboard**

***Project Overview***

This project analyzes customer churn behavior for a telecommunications company using Power BI. The dashboard identifies key drivers of customer attrition and evaluates the financial impact of churn to support data-driven retention strategies.

The analysis explores churn patterns across customer tenure, contract types, services used, demographics, and regional performance. The data model is built using a Snowflake Schema, with key metrics developed in DAX, and includes Row-Level Security (RLS) to simulate enterprise-level access control.

The analysis focuses on answering three critical business questions:

*Who is leaving? (Demographic & Tenure analysis)*

*Why are they leaving? (Service quality & Contractual friction)*

*What is the financial impact? (Revenue loss & LTV forecasting)*

Key insights reveal that customers with month-to-month contracts and shorter tenure periods are significantly more likely to churn, while service issues such as poor support expertise, network reliability, and pricing concerns are major churn drivers.

**Dashboard Preview**

*Executive Summary* 
<p align="center"> <img src="Images/1_Executive Summary.png" width="1200"> </p>

Provides a high-level overview of churn performance including **total customers, churn rate, revenue impact, churn trends, and key churn reasons.**

*Customer Tenure & Financial Performance*
<p align="center"> <img src="Images/2_Customer Tenure and Financial Performance.png" width="1200"> </p>

Analyzes how customer tenure influences churn probability and revenue impact, including monthly churned revenue, retention rate, and customer lifetime value (LTV).

*Services & Contracts*
<p align="center"> <img src="Images/3_Services and Contracts.png" width="1200"> </p>

Examines how **contract types, internet services, streaming features, and support services influence churn behavior and customer retention.**

*Customer Demographics*
<p align="center"> <img src="Images/4_Customers Demographics.png" width="1200"> </p>

Geographic heatmaps and age-based distribution identifying Texas and senior citizens (65+) as high-risk segments.

**🏗️ Data Architecture: Snowflake Schema**

To ensure high data integrity and optimized performance, the project utilizes a Snowflake Schema. This normalized approach allows for granular analysis of service tiers (Phone, Internet, Add-ons) without compromising report speed.

<p align="center"> <img src="Data Modeling - Snowflake Schema/Snowflake_Schema_Data_Modeling.png" width="1200"> </p>

📈 **Key Business Insights**

**The "Early Exit" Risk:** Customers in their first 6 months have a 17.82% churn rate, suggesting a need for better onboarding or introductory offers.

**Service Friction:** "Poor expertise of phone support" is the #1 reason for churn, accounting for the highest revenue loss ($2,596/month).

**Contractual Impact:** Month-to-month contracts exhibit significantly higher churn compared to one- or two-year commitments.

**Geographic Hotspots:** Texas leads the churn rate at 3.41%, indicating potential regional service or pricing competition issues.

💡 **Recommendations**

**Enhance Customer Support:** Targeted training for phone support teams to address the leading cause of dissatisfaction.

**Incentivize Long-term Contracts:** Move month-to-month users toward annual plans through loyalty discounts.

**Targeted Retention for Seniors:** Create specialized support or simplified billing for the 65+ demographic, which represents the largest active customer block but shows increasing churn sensitivity.
