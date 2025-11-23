# 📊 **Amazon Sales Analytics Dashboard — Power BI + SQL + Python Project**

## 📘 *MBA IT — Data Analytics Project*

### 👨‍🎓 **Student**

- **Shlok Tilokani** (ID: 24030141072)

---

![Amazon Sales Analytics Dashboard](res/video.gif)

---

## 🔍 **Project Overview**

This project is a complete **end‑to‑end Business Intelligence solution** built using:

- **Power BI** (Data import, modeling, OLAP, visual analytics)
- **MySQL** (Data storage + SQL OLAP queries)
- **Python (inside Power BI)** → Machine Learning (Profit Prediction)

The goal was to design a **dynamic, analytics‑driven dashboard** for **Amazon Sales Data**, combining:

- OLAP reporting  
- Forecasting  
- ML‑based predicted profit  
- Relational modeling  
- Business KPIs & Trend Visualization

No external IDE or Notebook was used—**all ML code was executed within Power BI itself**.

---

## 🌱 **Nature of Dataset**

The dataset was stored in **MySQL** and imported into Power BI. The database structure is visible in the SQL dump. Key attributes include:

### **🔹 Data Table Fields**

- `Order ID`
- `Order Date`
- `Ship Date`
- `EmailID`
- `Geography`
- `Category`
- `Product Name`
- `Sales`
- `Quantity`
- `Profit`

### **📦 Additional Derived Tables (via SQL & Python)**

- **OLAP1: Sales_By_Category** → `Category`, `TotalProfit`
- **OLAP2: Top_10_by_Sales** → `Product Name`, `TotalSales`
- **PythonData (SampleOutput)** → row-level predictions
- **PythonData (GroupedOutput)** → aggregated predictions category-wise

Dataset Size: **1000+ rows**, 14 columns.

---

## ⚙️ **Project Workflow**

## **1️⃣ Data Loading (MySQL → Power BI)**

Two SQL queries were used to generate OLAP tables.

### **🔹 Sales by Category Query** (OLAP1)

```sql

SELECT
Category,
SUM(Profit) AS TotalProfit
FROM data
GROUP BY Category
ORDER BY TotalProfit DESC;

```

### **🔹 Top 10 Products by Sales Query** (OLAP2)

```sql

SELECT
`Product Name`,
SUM(Sales) AS TotalSales
FROM data
GROUP BY `Product Name`
ORDER BY TotalSales DESC
LIMIT 10;

```

These tables were loaded directly into Power BI using the **MySQL connector**.

---

## **2️⃣ Power Query Transformations**

Inside **Power Query Editor**, transformations applied:

- Removed unnecessary columns
- Split Geography into Country → State → City
- Converted data types (dates, decimals)
- Created custom columns for analysis
- Ensured clean schema before modeling

Applied steps are visible in screenshots.

---

## **3️⃣ Data Modeling in Power BI**

A **star-schema-inspired model** was created.

### **Tables Used:**

- `Data` (Fact table)
- `OLAP1: Sales_By_Category` (Dimension)
- `OLAP2: Top_10_by_Sales` (Dimension)
- `PythonData(GroupedOutput)` (ML output)
- `PythonData(SampleOutput)` (ML predictions)

### **Relationships:**

- Category → Category (1:* mapping)
- Product Name → Product Name
- Category links across Python and OLAP tables

This allowed combined insight using **SQL + Python + BI visuals**.

---

## **4️⃣ Machine Learning in Power BI (Python Script)**

A **Random Forest Regressor** was trained INSIDE Power BI using the built-in Python environment.

### **Model Objective:**

Predict **Profit** using:

- Sales
- Quantity
- Category
- Product Name
- Geography

### **Key Model Features:**

- OneHotEncoding for categorical columns
- sklearn Pipeline
- RandomForestRegressor (n_estimators=100)

### **Python Script Used (for Grouped Output)**

```python

# Full script available in project

model = Pipeline([...])
model.fit(X, y)
df['PredictedProfit'] = model.predict(X)
df['Error'] = df['Profit'] - df['PredictedProfit']

# dataset = sample_output

dataset = grouped_output

```

### **Output Returned to Power BI**

- Profit by Category
- Predicted Profit by Category
- Average Error

This ML output was merged into the final dashboard.

---

## **5️⃣ OLAP Operations**

Performed directly using SQL & Power Query:

- **Roll-up:** Category → Total Profit
- **Drill-down:** Product-level sales
- **Aggregation:** SUM(Sales), SUM(Profit)
- **Sorting & Ranking:** Top 10 products

These processed tables strengthened dashboard analysis.

---

## **6️⃣ Power BI Visualizations**

The dashboard contains:

### **🔹 KPI Cards**

- Total Orders = 3099
- Total Quantity = 11.84K
- Total Profit = 106.02K
- Total Sales = 713.47K

### **🔹 Regression Plot**

Scatter chart showing:

- Actual Profit vs Predicted Profit
- Almost linear upward trend (strong prediction)

### **🔹 Category Comparison (Line Chart)**

Compares:

- Average Profit
- Average Predicted Profit

### **🔹 Year‑wise Sales Trend**

Shows growth from 2011 → 2014.

### **🔹 Treemap**

Sales by Category (Chairs, Phones, Binders, etc.)

### **UI Theme:**

Custom Amazon-style **yellow-orange theme**.

---

## 🧪 **7️⃣ Insights & Findings**

- **Random Forest model predicts Profit accurately** with low average error.
- **Phones, Chairs, Tables** are highest selling categories.
- **Some products show negative profit**, requiring operational attention.
- **Strong relationship between Sales and Profit** visible in scatter plot.
- **Yearly Sales** show continuous improvement.
- **Category segmentation** reveals the most profitable segments.

---

## 🏁 **Conclusion**

This project demonstrates a fully integrated BI + ML system:

- **SQL** for data extraction & OLAP
- **Power BI** for cleaning, modeling, and dashboarding
- **Python** inside Power BI for machine learning

📌 The final dashboard provides actionable insights for Amazon‑style retail data, combining business intelligence with predictive analytics.

---

## 🚀 **Future Enhancements**

- Deploy ML model via Azure ML Web API
- Integrate forecasting using Power BI AutoML
- Add DAX measures for deeper KPI insight
- Publish dashboard to Power BI Service

---

## 📦 **Project Files**

- `Dump20250907.sql` — MySQL database dump (raw data)
- `data.xlsx` — Excel source (Power Query transformations)
- Power BI `.pbix` dashboard (contains SQL + Python + visuals)

---

## ⭐ **Thank You!**

If this dashboard inspired you, feel free to ⭐ star the repository!
