# 📊 HR Analytics - Employee Attrition Analysis Dashboard

### 🚀 Project Overview
This project is an end-to-end, interactive **HR Analytics & Employee Attrition Dashboard** developed in **Microsoft Power BI**. Using a real-world dataset of **1,480 employee records**, this dashboard transforms raw HR data into actionable workforce retention insights. It empowers HR teams and stakeholders to evaluate turnover drivers, monitor high-risk job roles, analyze compensation impacts, and improve employee retention through dynamic visual storytelling.

---

## 🛠️ Technical Challenges & Solutions

During the data modeling and dashboard development phase, several technical challenges were resolved to ensure 100% data accuracy and a clean user interface:

#### 1. Converting Categorical Target Variable (`Attrition` as "Yes" / "No")
*   **Problem:** The primary target column (`Attrition`) contained text strings (`"Yes"` and `"No"`), which prevented direct mathematical aggregations for total departures.
*   **Solution:** Engineered a custom **DAX Calculated Column** (`Attrition Count = IF(HR_Analytics[Attrition] = "Yes", 1, 0)`) to convert text values into binary numerical indicators (`1` and `0`).

#### 2. Dynamic Attrition Rate Calculation Across Filters
*   **Problem:** Static percentage calculations fail to update dynamically when slicing data across multiple departments or demographics.
*   **Solution:** Created a dynamic **DAX Measure** (`Attrition Rate = SUM(HR_Analytics[Attrition Count]) / SUM(HR_Analytics[EmployeeCount])`) formatted as a percentage (`16.08%`) to respond accurately to cross-filtering.

#### 3. Resolving Axis Scale Disparity & Data Noise
*   **Problem:** Plotting `Attrition Count` (whole numbers) and `Attrition Rate` (percentages) on a single axis flattened the trend line. Additionally, an unclean `TravelRarely` entry created a `0` value bar in the Business Travel chart.
*   **Solution:** Mapped `Attrition Rate` to a Secondary Line Y-axis in a Combo Chart with conditional gradient colors, and applied a visual-level filter (`> 0`) to remove zero-value noise.

---

## 📈 Dashboard Pages & Visual Breakdown

This single-page, interactive dashboard contains **6 KPI Cards**, **8 Core Analytical Visuals**, and **4 Dynamic Slicers**:

1.  **Executive KPI Cards (6 Cards):** Displays top-level metrics at a glance — **Count of Employee (`1.48K`)**, **Attrition (`238`)**, **Attrition Rate (`16.08%`)**, **Avg Age (`36.92`)**, **Avg Salary (`6.50K`)**, and **Avg Tenure (`7.01` years)**.
2.  **Attrition Count by Gender (Donut Chart):** Shows turnover distribution between **Male (`151`)** and **Female (`87`)** employees.
3.  **Attrition by Education (Pie Chart):** Highlights that **Life Sciences (`89`)** and **Medical (`63`)** fields experience the highest turnover, while **Human Resources (`7`)** has the lowest.
4.  **Attrition Count and Rate by Age Group (Combo Chart):** Reveals that the **26–35 age group** has the highest departure volume (`116`), whereas the **18–25 age group** has the highest attrition rate.
5.  **Job Role and Level wise Attrition Count (Matrix Chart):** Pinpoints **Level 1 (`143` departures)** as the most vulnerable tier, primarily among **Laboratory Technicians (`62`)** and **Research Scientists (`47`)**.
6.  **Attrition by Marital Status (Pie Chart):** Demonstrates that **Single employees (`120`)** have a higher turnover volume compared to **Married (`84`)** and **Divorced (`34`)** staff.
7.  **Attrition Count by Salary Slab & YearsAtCompany (Bar & Area Charts):** Proves that the **Upto 5k** salary bracket (`163` departures) and **Year 1** tenure (`59` departures) are the most critical turnover points.
8.  **Attrition by Department & Business Travel (Bar & Column Charts):** Shows **R&D (`133`)** and **Sales (`93`)** leading in departmental turnover, with **Travel_Rarely (`157`)** accounting for the highest travel-based attrition.

---

## 📁 Repository Contents

*   `HR_Analytics_Dashboard.pbix` : The fully functional Power BI dashboard containing the data model, custom DAX calculations, and interactive visuals.
*   `HR_Analytics.csv` : The raw dataset used for this project.
*   `HR Analytics Dashboard - Employee Attrition Analysis.png` : A high-resolution image preview of the completed dashboard.
*   `HR Analytics Dashboard - Employee Attrition Analysis.pdf` : A static PDF export of the complete dashboard for quick review.
*   `BG12.jpg` : The custom canvas background image used in the dashboard.

---

## 👨‍💻 Author

**Bayzid Mostak**<br>
*Data Analyst & Visualization Expert*

*   [LinkedIn] https://www.linkedin.com/in/bayzid-mostak-data-analyst/
*   [GitHub] https://github.com/TusharAlBayzid
*   Note: Download the `.pbix` file and open it in Power BI Desktop to experience the fully interactive cross-filtering capabilities of this dashboard.
