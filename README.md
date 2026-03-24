# 🏡 Airbnb Performance Dashboard

## 📚 About Data

Data source: https://mavenanalytics.io/data-playground/airbnb-listings-reviews 


This project analyzes Airbnb listing data across multiple global cities, focusing on pricing, customer satisfaction, host performance, and market distribution.

The dataset includes key attributes such as:

* Listing details (price, room type, host status)
* Review scores (accuracy, cleanliness, communication, location, value)
* City-level distribution of listings
* Superhost classification

The dataset enables comparison of **customer experience vs pricing**, **market concentration**, and **host performance trends** across cities.

---

## 💡 Highlights

* 🌍 **Mexico City and Rio de Janeiro lead in customer satisfaction**, achieving the highest overall ratings (~94–95%).
* 📉 **Hong Kong and Istanbul rank lowest**, driven by weaker cleanliness and value scores.
* 💸 **Cape Town and Bangkok have the highest prices**, suggesting premium/luxury positioning despite lower supply.
* 🏙️ **Paris and New York dominate in listing volume**, but do not lead in ratings — showing that popularity ≠ best experience.
* ⭐ **Superhosts consistently outperform**, maintaining higher ratings despite representing a smaller share of listings.
* ⚖️ **Strong inverse relationship between price and availability**, indicating supply-demand dynamics across cities.
* 🧼 **Cleanliness and value are the weakest metrics globally**, highlighting key improvement areas.

---

### 📐 Key DAX Measures

```DAX
-- Accuracy Score
Accuracy = AVERAGE(Listings[review_scores_accuracy])

-- Average Price
avg price = AVERAGE(Listings[price])

-- Total Listings
total listings = COUNT(Listings[listing_id])

-- Superhost Listings
superhost listings = 
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[host_is_superhost] = "t"
)

-- City Rank
city rank = 
RANKX(
    ALL(Listings[city]),
    [total listings],
    ,
    DESC
)

-- Cumulative Listings
cummulative listings =
VAR currentrank = MAXX(VALUES(Listings[city]), [city rank])
RETURN
CALCULATE(
    [total listings],
    FILTER(
        ALL(Listings[city]),
        [city rank] <= currentrank
    )
)
```

✔️ Additional measures created for each **room type (Entire, Private, Shared, Hotel)** to enable dynamic and customizable visuals.

---

## 📊 Visualization
<img width="962" height="723" alt="Screenshot 2026-03-24 121940" src="https://github.com/user-attachments/assets/153962ce-80fe-400e-a7b2-924f6d91f67f" />

<img width="1282" height="725" alt="Screenshot 2026-03-24 121954" src="https://github.com/user-attachments/assets/25c05680-4ceb-4270-b52e-13ae56d1ed0f" />

<img width="1281" height="722" alt="Screenshot 2026-03-24 122011" src="https://github.com/user-attachments/assets/912626e6-57c6-47e5-b4e9-db945f2db177" />

<img width="1282" height="721" alt="Screenshot 2026-03-24 122026" src="https://github.com/user-attachments/assets/e43bec7c-cb62-40eb-9392-e85cbbeea63e" />

Developed an interactive **Power BI dashboard** with the following views:

* 📌 **KPI Overview**

  * Total Listings, Cities, Hosts, Property Types, Reviews

* 📈 **Listings Growth Over Time**

  * Lifecycle phases: Introduction → Growth → Maturity → Decline → Reinvention → COVID impact

* 🌆 **City-Level Analysis**

  * Average ratings across multiple dimensions
  * Ranking of cities based on performance

* 💰 **Pricing Insights**

  * Average price across cities
  * Price comparison by room type

* 📊 **Market Share Analysis**

  * Distribution of listings by city
  * Superhost vs non-superhost contribution
  * Cumulative market share

---

## 🔍 Key Insights

* High supply cities are not necessarily top-rated → **quality vs scale trade-off**
* Superhosts play a critical role in **maintaining platform quality**
* Pricing varies significantly by geography → **market positioning differs across cities**
* COVID caused a **sharp drop in listings**, disrupting steady growth trends
* **Customer satisfaction is most sensitive to cleanliness and perceived value**

---

## 📍 Files in Repository

* `Airbnb_Dashboard.pbip` → Power BI dashboard file
* `listings_data_dictionary.csv` → Data dictionary for the Raw dataset
* `README.md` → Project documentation

---

## 🚀 Tools Used

* Power BI (Data Modeling & Visualization)
* DAX (Measures & Calculations)
* Excel/CSV (Data Source)

---
