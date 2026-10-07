# 📊 HR Analytics - Employee Attrition Analysis Dashboard

### 🚀 Project Overview
This project is an end-to-end, interactive **HR Analytics & Employee Attrition Dashboard** developed in **Microsoft Power BI**[cite: 17]. Using a comprehensive dataset of **1,480 employee records across 38 distinct attributes**[cite: 1, 5, 17], this dashboard transforms raw human resource data into actionable workforce retention insights. It empowers HR leaders and organizational stakeholders to identify key drivers of employee turnover, analyze demographic and compensation patterns, monitor high-risk job roles, and formulate data-driven retention strategies through dynamic visual storytelling[cite: 17].

---

## 🛠️ Technical Challenges & Solutions

During the data extraction, transformation, DAX modeling, and dashboard design phases, several technical challenges were systematically resolved to ensure 100% data accuracy and an executive-ready user interface:

#### 1. Categorical Text Target Variable (`Attrition` as "Yes" / "No")
*   **Problem:** The primary target column, `Attrition`, was stored as categorical text strings (`"Yes"` and `"No"`)[cite: 1], making it impossible to directly perform mathematical aggregations (such as summing total departures or calculating turnover ratios across dimensions).
*   **Solution:** Engineered a custom **DAX Calculated Column** named `Attrition Count` using conditional logic:  
    `Attrition Count = IF(HR_Analytics[Attrition] = "Yes", 1, 0)`[cite: 5]  
    This converted the binary text column into a numerical indicator (`1` for departed employees, `0` for active employees), enabling seamless aggregation across all visuals[cite: 5, 17].

#### 2. Dynamic Attrition Rate Calculation Across Filter Contexts
*   **Problem:** Calculating a static attrition percentage would fail to update dynamically when users slice the data by specific departments, age groups, or education fields[cite: 17].
*   **Solution:** Created a dynamic **DAX Measure** named `Attrition Rate` by dividing the sum of departed employees by the total workforce count:  
    `Attrition Rate = SUM(HR_Analytics[Attrition Count]) / SUM(HR_Analytics[EmployeeCount])`[cite: 5, 6]  
    Formatted the measure explicitly as a **Percentage (`%`)** with 2 decimal places (`16.08%`) so it responds accurately to every interactive filter[cite: 5, 17].

#### 3. Scale Disparity Between Attrition Volume & Rate in Age Group Analysis
*   **Problem:** Plotting `Sum of Attrition Count` (whole numbers up to `116`) alongside `Attrition Rate` (percentages from `0%` to `40%`) on a single axis caused the percentage values to flatten along the bottom of the chart[cite: 9, 17].
*   **Solution:** Implemented a **Dual-Axis Combo Chart (Line and Stacked Column Chart)** where `Sum of Attrition Count` is mapped to the primary Column Y-axis and `Attrition Rate` is mapped to the secondary Line Y-axis[cite: 9, 17]. Additionally, applied conditional gradient formatting (`fx`) on the columns to visually highlight high-volume turnover brackets[cite: 9, 17].

#### 4. Data Inconsistency & Zero-Value Noise in `BusinessTravel` Category
*   **Problem:** The `BusinessTravel` dimension contained a duplicate/unclean text entry without an underscore (`TravelRarely` alongside `Travel_Rarely`), which generated an empty category with `0` attrition count and cluttered the X-axis[cite: 14, 15, 16].
*   **Solution:** Applied a visual-level filter (`Sum of Attrition Count is greater than 0`) on the Business Travel column chart to strip out zero-value noise, leaving only the 3 valid categories (`Travel_Rarely`, `Travel_Frequently`, and `Non-Travel`)[cite: 17].

#### 5. Visual Clutter & Label Truncation on Dark Custom Canvas
*   **Problem:** Placing multiple dense visuals over a dark gradient background (`BG12`) caused low text contrast, while long percentage strings inside smaller Donut/Pie charts resulted in truncated labels (`...`)[cite: 16, 17, 19].
*   **Solution:** Standardized all chart containers with **85% background transparency**, **`12px` rounded white borders**, and high-contrast yellow/white typography. Simplified pie/donut detail labels to display exact `Data values` and optimized matrix font sizing to maximize readability[cite: 17].

---

## 📈 Dashboard Pages & Visual Breakdown

This single-page, highly interactive dashboard comprises **6 Executive KPI Cards**, **8 Core Analytical Visuals**, and **4 Dynamic Slicers** integrated for seamless cross-filtering[cite: 17]:

#### 📌 Top-Level Executive KPIs (6 Card Visuals)
Provides an immediate high-level snapshot of organizational health[cite: 17]:
*   **Count of Employee:** `1.48K` (`1,480` total workforce)[cite: 5, 17]
*   **Attrition:** `238` (total employees who left the company)[cite: 17]
*   **Attrition Rate:** `16.08%` (overall organizational turnover rate)[cite: 17]
*   **Avg Age:** `36.92` years[cite: 17]
*   **Avg Salary:** `6.50K` (average monthly income)[cite: 17]
*   **Avg Tenure:** `7.01` years (average years spent at the company)[cite: 17]

#### 📊 Core Analytical Visuals (8 Charts)
1.  **Attrition Count by Gender (Donut Chart):** Breaks down departures by gender, revealing that **Male employees (`151`)** account for a significantly higher volume of attrition compared to **Female employees (`87`)**[cite: 17].
2.  **Attrition by Education (Pie Chart):** Evaluates turnover across academic backgrounds[cite: 17]. Highlights that **Life Sciences (`89`)** and **Medical (`63`)** fields experience the highest attrition, followed by **Marketing (`36`)**, **Technical Degree (`32`)**, **Other (`11`)**, and **Human Resources (`7`)**[cite: 17].
3.  **Attrition Count and Rate by Age Group (Combo Column & Line Chart):** Compares total departures (bars) against turnover rate (line) across age brackets[cite: 17]. Reveals a critical insight: while the **26–35 age group** has the highest *volume* of departures (`116`), the younger **18–25 age group** suffers from the highest *rate* of attrition (~`35.8%`)[cite: 17].
4.  **Job Role and Level wise Attrition Count (Conditional Matrix Chart):** A cross-tabulated matrix mapping `JobRole` against `JobLevel` (`1` to `5`)[cite: 17]. Pinpoints that **Level 1 (`143` total departures)** is the most vulnerable tier, heavily concentrated among **Laboratory Technicians (`62` total; `56` at Level 1)** and **Research Scientists (`47` total; `45` at Level 1)**[cite: 17].
5.  **Attrition by Marital Status (Pie Chart):** Demonstrates that **Single employees (`120`)** leave the organization at a much higher frequency than **Married (`84`)** and **Divorced (`34`)** employees[cite: 17].
6.  **Attrition Count by Salary Slab (Horizontal Stacked Bar Chart):** Analyzes the impact of compensation on retention[cite: 17]. Proves that lower income is a primary turnover catalyst, with the **Upto 5k** slab accounting for **`163` departures** (nearly 68.5% of all attrition), compared to **5k–10k (`49`)**, **10k–15k (`21`)**, and **15k+ (`5`)**[cite: 17].
7.  **Attrition Count by YearsAtCompany (Area Chart):** Tracks employee departures across their tenure lifecycle[cite: 17]. Identifies a massive early-tenure spike at **Year 1 (`59` departures)** and secondary peaks around **Years 2–5** and **Year 10 (`18`)**, indicating onboarding and early-career retention challenges[cite: 17].
8.  **Attrition Count by Department (Horizontal Bar Chart) & Business Travel (Vertical Column Chart):**
    *   **Department:** Shows **Research & Development (`133`)** and **Sales (`93`)** leading in total departures, while **Human Resources (`12`)** remains minimal[cite: 17].
    *   **Business Travel:** Highlights that employees who **Travel_Rarely (`157`)** and **Travel_Frequently (`69`)** account for the vast majority of departures compared to **Non-Travel (`12`)** staff[cite: 17].

#### 🎛️ Interactive Filter Panel (4 Dropdown Slicers)
Located along the bottom row, allowing users to dynamically slice the entire report by **`AgeGroup`**, **`BusinessTravel`**, **`Department`**, and **`EducationField`**[cite: 17].

---

## 📁 Repository Contents

*   `HR_Analytics_Dashboard.pbix` : The fully functional Power BI dashboard file containing the data model, custom DAX column/measure, and interactive visuals[cite: 5, 17, 19].
*   `HR_Analytics.csv` : The raw HR analytics dataset (1,480 rows, 38 columns) used for this project[cite: 1, 5, 19].
*   `HR Analytics Dashboard - Employee Attrition Analysis.png` : A high-resolution image preview of the completed dashboard.
*   `HR Analytics Dashboard - Employee Attrition Analysis.pdf` : A static PDF export of the complete dashboard for quick executive review[cite: 19].
*   `BG12.jpg` : The custom 16:9 dark gradient canvas background image used in the report design[cite: 17, 19].

---

## 👨‍💻 Author

**Bayzid Mostak**<br>
*Data Analyst & Visualization Expert*

*   [LinkedIn] https://www.linkedin.com/in/bayzid-mostak-data-analyst/
*   [GitHub] https://github.com/TusharAlBayzid
*   Note: Download the `.pbix` file and open it in Power BI Desktop to experience the fully interactive cross-filtering capabilities of this dashboard.
