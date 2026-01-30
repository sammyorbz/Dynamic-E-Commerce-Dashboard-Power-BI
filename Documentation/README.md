# 📊 Dynamic E-Commerce Dashboard (Power BI)
## Process Documentation

This document outlines the **end-to-end process** used to build a **single-page, fully dynamic Power BI dashboard** using field parameters, time intelligence, and advanced visual formatting.

The emphasis of this project is **process over visuals** — focusing on how data is loaded, modeled, transformed, measured, and presented in a scalable BI workflow.

---

## 1️⃣ Project Objective
The goal of this project was to create a **one-page interactive dashboard** that allows users to:
- Switch between multiple business metrics (Sales, Profit, Profit Margin, Quantity, Average Discount)
- View Year-over-Year (YoY) performance dynamically
- Analyze performance by time, geography, customer segments, and product hierarchy
- Highlight key trends such as **highest-performing months and categories**

Rather than building multiple report pages, **field parameters** were used to control metric switching across the entire dashboard.

---

## 2️⃣ Data Loading
- The dataset used is a cleaned **e-commerce sales dataset (~50,000 rows)** in CSV format.
- Data was loaded directly into Power BI using **Get Data → CSV**.
- Since the dataset was already clean, **Power Query transformations were minimal**.

Key columns included:
- Order Date
- Customer details (Age, Gender, Segment)
- Geography (Market, Region, Country, State, City)
- Product hierarchy (Category, Subcategory, Product)
- Metrics (Sales, Profit, Quantity, Discount)

---

## 3️⃣ Calculated Columns
### Age Grouping
A calculated column was created to bucket customer ages into ranges for better segmentation:

- 20–30
- 31–40
- 41–50
- 51–60

This was implemented using a `SWITCH(TRUE())` logic to assign age bands dynamically.

---

## 4️⃣ Date Table Creation
To enable **time intelligence**, a dedicated **Calendar table** was created using DAX:

- Auto-generated date range
- Columns added:
  - Year
  - Quarter (formatted as Q1–Q4)
  - Month Name
  - Month Number

The Calendar table was related to the dataset via **Order Date** using a **one-to-many** relationship.

---

## 5️⃣ Data Model Structure
The final model consisted of:
- Fact table: E-commerce Data
- Dimension tables:
  - Calendar
  - Customer attributes (embedded)
- A dedicated **Measures Table** to store all DAX measures

This structure improves:
- Model readability
- Measure organization
- Maintainability

---

## 6️⃣ Core Measures (DAX)
Key aggregate measures created:
- Total Sales
- Total Profit
- Profit Margin
- Total Quantity
- Average Discount

Each measure was formatted appropriately (Currency, Percentage, Whole Number).

All measures were grouped into folders for clarity.

---

## 7️⃣ Year-Over-Year (YoY) Logic
Dynamic YoY calculations were created **without hardcoding previous year values**.

### YoY Logic Flow:
1. Identify the selected year
2. Calculate the previous year value
3. Compute the percentage change
4. Format the output as text with:
   - `+` sign for increases
   - Automatic negative sign for decreases
5. Return blank where no prior-year data exists

This logic ensures:
- Clean visuals
- No misleading values
- Better user interpretation

---

## 8️⃣ YoY Color Coding
Custom measures were created to:
- Display **green** for positive YoY change
- Display **red** for negative YoY change

These color measures were applied using **conditional formatting** on visuals.

---

## 9️⃣ Field Parameters (Metric Switching)
A **Field Parameter** was created to allow users to switch between:
- Sales
- Profit
- Profit Margin
- Average Discount
- Quantity

This parameter controls:
- KPI values
- Charts
- Titles
- Highlights
- Conditional formatting

The parameter order was intentionally defined to drive logic across:
- Labels
- Titles
- Conditional measures

---

## 🔟 Dynamic KPI Labels
A dynamic KPI label measure was created using:
- `SELECTEDVALUE()`
- Parameter order
- `SWITCH()` logic
- `FORMAT()` function

This allowed:
- Currency formatting for Sales & Profit
- Percentage formatting for margins
- Numeric formatting for Quantity

These labels power the **button slicer KPIs**.

---

## 1️⃣1️⃣ Button Slicer Configuration
Instead of traditional slicers:
- **Button slicers** were used
- Buttons were styled to behave like KPI cards
- Selected button shows:
  - Darker fill
  - Border highlight
  - Selection icon
- Non-selected buttons appear muted

This improves usability and visual clarity.

---

## 1️⃣2️⃣ Visuals & Charts
### Charts Created:
- Monthly trend (column chart)
- Market → Region → Country drill-down bar chart
- Segment distribution (donut chart)
- Product hierarchy (treemap)

All charts are:
- Driven by the field parameter
- Fully synchronized
- Free from duplicated measures

---

## 1️⃣3️⃣ Highlighting Top Performers
A custom measure was created using:
- `MAXX()`
- `ALLSELECTED()`
- Parameter order logic

This highlights:
- The **highest-performing month** for the selected metric
- With a distinct color

All other values appear muted.

---

## 1️⃣4️⃣ Handling Negative Values
For Profit and Profit Margin:
- Negative values were highlighted using a contrasting color (e.g., pink/red)
- Positive values retained the primary dashboard color

This ensures financial losses are easily identifiable.

---

## 1️⃣5️⃣ Dynamic Titles
A dynamic title measure was created to reflect the currently selected metric.

Titles update automatically when users switch metrics via the button slicer.

---

## 1️⃣6️⃣ Slicers
Additional slicers were added:
- Year
- Age Group
- Gender

All slicers were styled consistently using copied formatting to maintain UI consistency.

---

## 1️⃣7️⃣ Final Layout & UX Refinement
Final steps included:
- Aligning visuals for consistent spacing
- Layering visuals correctly (cards behind slicers where required)
- Disabling unnecessary visual interactions
- Removing visual clutter (borders, gridlines, unused legends)

---

## 1️⃣8️⃣ Key Takeaways
- Field Parameters enable powerful **single-page dashboards**
- Separating measures improves model clarity
- Dynamic formatting enhances storytelling
- One well-designed page can replace multiple report tabs

---

## ⚠️ Disclaimer
This dashboard was recreated as part of a **learning workshop**.
The implementation reflects independent analytical understanding and is intended for **portfolio and educational use only**.

---

📌 *Built with Power BI using advanced DAX, Field Parameters, and Time Intelligence*
