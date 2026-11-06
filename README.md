<h1 align="center">🛍️ Myntra Sales & Product Dashboard</h1>

<p align="center">
  <b>An interactive two-page Power BI dashboard on Myntra order and product data</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Tool-Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" />
  <img src="https://img.shields.io/badge/Orders-1,80,000-6A1B9A?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Products-2,500-1E6FD0?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Pages-2-2E7D32?style=for-the-badge" />
</p>

<p align="center"><b>Data as of: 03/11/2026</b></p>

---

## 📌 Table of Contents

1. [Project Overview](#-project-overview)
2. [Dashboard Screenshots](#-dashboard-screenshots)
3. [Page 1: Sales Overview](#-page-1-sales-overview)
4. [Page 2: Product Analysis](#-page-2-product-analysis)
5. [Interactivity](#-interactivity)
6. [Dataset](#-dataset)
7. [Data Preparation](#-data-preparation-power-query)
8. [Data Model](#-data-model)
9. [DAX Measures](#-dax-measures)
10. [Key Observations](#-key-observations)
11. [Business Recommendations](#-business-recommendations)
12. [Design](#-design)
13. [How to Use](#-how-to-use)
14. [Notes](#-notes)
15. [Achievements](#-project-highlights--achievements)
16. [Skills Demonstrated](#-skills-demonstrated)
17. [Future Enhancements](#-future-enhancements)
18. [Author](#-author)

---

## 🎯 Project Overview

This is an interactive, two-page Power BI dashboard built on Myntra order and product data. It shows order volume, revenue, brand and category performance, city-tier split, size-wise inventory, and order status. Slicers and cross-filtering let every number be explored by brand, category and city tier.

**Objectives**

- Track total orders and revenue at a glance
- Compare brands, categories and city tiers
- Understand product and size-wise inventory
- Monitor order status (Delivered, Shipped, Returned, Cancelled)

---

## 🖼️ Dashboard Screenshots

### Page 1: Sales Overview

<img width="1197" height="676" alt="Page 1" src="https://github.com/user-attachments/assets/a20b52e1-1242-4734-9ae1-04de3d25348c" />

### Page 2: Product Analysis

<img width="1207" height="682" alt="Page 2" src="https://github.com/user-attachments/assets/70a6e9f5-5231-46c9-ab5d-a879e3c5ec9d" />

---

## 📊 Page 1: Sales Overview

A quick view of overall sales performance.

| Section | Details |
|---|---|
| **Slicers** | Brand_Name, Category, City_Tier |
| **KPI Cards** | Total Orders (180K), Total Revenue (₹ 118.90 Cr) |
| **Donut Chart** | Total Orders by City Tier |
| **Column Chart** | Total Orders by Category (13 categories) |
| **Bar Chart** | Total Orders by Brand (10 brands) |

---

## 📦 Page 2: Product Analysis

A deeper look at products, brands, inventory and order status.

| Section | Details |
|---|---|
| **Product Distribution** | Donut chart of product count (SKU) by category |
| **Size-wise Inventory** | Column chart of inventory units by size (XS, S, M, L, XL) |
| **Brand Performance** | Bar chart of revenue (₹ Cr) by brand |
| **City Tier Analysis** | Column chart of revenue (₹ Cr) by city tier |
| **Top Products by Revenue** | Table with Product Name, Brand, Category, Total Orders, Total Revenue |
| **Order Status Distribution** | Donut chart of Cancelled, Shipped, Returned and Delivered orders |

**Navigation:** A left-hand navigation bar switches between Page 1 and Page 2. Page 2 also has a "Back to Page 1" button.

---

## 🔗 Interactivity

- All visuals on a page are linked to each other.
- Selecting a value in a slicer updates the cards and charts.
- Clicking a bar, column or donut slice cross-filters the other visuals.
- Cards and totals recalculate for the current selection.

---

## 🗂️ Dataset

**Files used**

| File | Rows | Used For |
|---|---|---|
| `myntra_orders_master.csv` | 1,80,000 | Orders, revenue, brand, category, city tier, order status, product table |
| `myntra_product_catalog.csv` | 2,500 | Product distribution and size-wise inventory |

**Files not used, and why**

| File | Reason |
|---|---|
| `myntra_festive_orders.csv`, `myntra_summer_orders.csv`, `myntra_winter_orders.csv` | These are subsets of the master file (their Order_IDs already exist in it). Loading them would double-count orders and revenue. |
| `myntra_web_catalog.csv` | Contains only ratings and review counts, which are not part of this dashboard. |

---

## 🧹 Data Preparation (Power Query)

1. **Brand_Name:** removed extra spaces and standardised capitalisation (for example `NIKE`, ` Nike` and `Nike` became `Nike`).
2. **Order_Date:** converted the different date formats into one Date type.
3. **Data types:** set correctly for date, whole number and decimal columns.
4. **Table names:** renamed to `Orders` and `Catalog`.
5. **SizeData table:** a small table holding total units for each size (XS, S, M, L, XL), used for the Size-wise Inventory chart.

---

## 🧩 Data Model

```
Catalog (SKU)  ──── One to Many ────>  Orders (SKU)
```

The relationship uses the SKU column with single-direction filtering. `SizeData` is a standalone table used only for the size chart.

---

## 🧮 DAX Measures

```DAX
Total Orders    = DISTINCTCOUNT(Orders[Order_ID])

Total Revenue   = SUM(Orders[Net_Revenue])

Revenue Cr      = DIVIDE([Total Revenue], 10000000)

Revenue Cr Text = "₹ " & FORMAT([Revenue Cr], "0.00") & " Cr"

Total Products  = DISTINCTCOUNT(Catalog[SKU])
```

---

## 🔍 Key Observations

| Area | Observation |
|---|---|
| **Overall** | 180K orders and ₹ 118.90 Cr in revenue |
| **City Tier (orders)** | Tier 2 has the largest share (49.97%), followed by Tier 1 (37.46%) and Tier 3 (12.57%) |
| **City Tier (revenue)** | Tier 2 leads with about ₹ 59.33 Cr, then Tier 1 (₹ 44.64 Cr) and Tier 3 (₹ 14.93 Cr) |
| **Category** | Kids Wear (23.9K) and School Shoes (21.8K) have the most orders; Handbags has the fewest (9.4K) |
| **Brand (orders)** | Nike has the most orders, and the 10 brands are fairly close to each other |
| **Brand (revenue)** | Nike leads with about ₹ 13.32 Cr, followed by Puma and HRX |
| **Inventory** | Size M has the highest inventory (about 0.50M units); XS and XL are the lowest (about 0.25M each) |
| **Order Status** | Orders are split almost evenly across Cancelled, Shipped, Returned and Delivered (about 25% each) |

---

## 💡 Business Recommendations

1. Focus marketing and delivery capacity on **Tier 2 cities**, which bring the highest share of orders and revenue.
2. Keep higher stock of **size M**, which has the highest inventory and is the most common size.
3. **Cancelled and Returned orders together are about 50%** of all orders. This is worth investigating to reduce losses.
4. Promote **Kids Wear and School Shoes**, the top categories by orders, and review low-order categories such as Handbags.
5. Brand revenue is fairly balanced, so offers can be planned brand by brand rather than relying on a single brand.

---

## 🎨 Design

- Dark navy header with the Myntra logo, page title and "Data as of" date.
- Dark purple left navigation bar with page icons.
- White cards with rounded borders on a light grey canvas.
- Colour palette: purple, green, blue, orange, teal and navy.

---

## ▶️ How to Use

1. Open the `.pbix` file in Power BI Desktop.
2. Use the slicers on Page 1 to filter by Brand, Category and City Tier.
3. Click any chart element to cross-filter the rest of the page.
4. Use the left navigation bar to move between Page 1 and Page 2.

---

## 📝 Notes

- The dataset has an order status of **Shipped** (there is no "Pending" status), so Shipped is shown on the Order Status chart.
- The category list in the data (for example Sneakers, School Shoes, Face Wash, Lipstick) is different from a typical fashion catalogue, so the charts show the real categories from the data.

---

## 🏆 Project Highlights & Achievements

- ✅ Built a complete 2-page interactive dashboard in Power BI
- ✅ Analysed 1,80,000 orders and 2,500 products
- ✅ Created 14 interactive elements: 3 slicers, 2 KPI cards and 9 charts / tables
- ✅ Spotted that 3 seasonal files duplicated the master data and excluded them to avoid double counting
- ✅ Cleaned inconsistent brand names and mixed date formats
- ✅ Designed a custom branded layout with header, logo, navigation bar and page buttons
- ✅ Connected two tables with a one-to-many relationship using SKU
- ✅ Wrote DAX measures for orders, revenue and product counts
- ✅ Turned the data into clear business recommendations

---

## 🛠️ Skills Demonstrated

![Power Query](https://img.shields.io/badge/Data%20Cleaning-Power%20Query-F2C811?style=flat-square)
![Data Modeling](https://img.shields.io/badge/Data%20Modeling-Relationships-6A1B9A?style=flat-square)
![DAX](https://img.shields.io/badge/DAX-Measures-1E6FD0?style=flat-square)
![Visualisation](https://img.shields.io/badge/Data-Visualisation-2E7D32?style=flat-square)
![Dashboard Design](https://img.shields.io/badge/Dashboard-Design-F5821F?style=flat-square)
![Business Analysis](https://img.shields.io/badge/Business-Analysis-0F8B8D?style=flat-square)

---

## 🚀 Future Enhancements

- [ ] Add a date slicer and monthly trend charts
- [ ] Add month-on-month and year-on-year growth indicators
- [ ] Add drill-through pages for product-level details
- [ ] Add a customer and delivery-time analysis page
- [ ] Create a mobile-friendly layout
- [ ] Publish the report to Power BI Service with scheduled refresh

---

## 👩‍💻 Author

| | |
|---|---|
| **Name** | Sneha Gupta |
| **Course** | [ Data Analysis ] |
| **Date** | 03/11/2026 |
| **GitHub** | [snehagupta47103-stack](https://github.com/snehagupta47103-stack) |

---

## 🙏 Acknowledgement

I would like to thank my teacher for the guidance and for giving me the opportunity to work on this project. It helped me learn how to turn raw data into a clear and interactive dashboard.

---

<p align="center"><b>⭐ Thank you for viewing this project! ⭐</b></p>
