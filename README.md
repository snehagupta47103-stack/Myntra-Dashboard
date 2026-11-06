╔══════════════════════════════════════════════════════════════╗
║        MYNTRA SALES & PRODUCT DASHBOARD  (POWER BI)          ║
╚══════════════════════════════════════════════════════════════╝

  Data as of : 03/11/2026
  Tool       : Microsoft Power BI Desktop
  Dataset    : 1,80,000 orders  |  2,500 products
  Pages      : 2  (Sales Overview, Product Analysis)


──────────────────────────────────────────────────────────────
1. PROJECT OVERVIEW
──────────────────────────────────────────────────────────────
This is an interactive, two-page Power BI dashboard built on Myntra
order and product data. It shows order volume, revenue, brand and
category performance, city-tier split, size-wise inventory, and
order status, with slicers and cross-filtering so that every number
can be explored by brand, category and city tier.

OBJECTIVES
  * Track total orders and revenue at a glance
  * Compare brands, categories and city tiers
  * Understand product and size-wise inventory
  * Monitor order status (Delivered, Shipped, Returned, Cancelled)


──────────────────────────────────────────────────────────────
2. DASHBOARD SCREENSHOTS
──────────────────────────────────────────────────────────────

PAGE 1: SALES OVERVIEW

<img width="1197" height="676" alt="Page 1" src="https://github.com/user-attachments/assets/d95fbb42-c8fe-4663-aa53-c7bb9b1f51b5" />









PAGE 2: PRODUCT ANALYSIS

<img width="1207" height="682" alt="Page 2" src="https://github.com/user-attachments/assets/708d41d1-703e-4e54-9c7d-3c90eb38eafd" />









──────────────────────────────────────────────────────────────
3. PAGE 1: SALES OVERVIEW
──────────────────────────────────────────────────────────────
Gives a quick view of overall sales performance.

  Slicers      : Brand_Name, Category, City_Tier
  KPI Cards    : Total Orders (180K), Total Revenue (Rs. 118.90 Cr)
  Donut Chart  : Total Orders by City Tier
  Column Chart : Total Orders by Category (13 categories)
  Bar Chart    : Total Orders by Brand (10 brands)


──────────────────────────────────────────────────────────────
4. PAGE 2: PRODUCT ANALYSIS
──────────────────────────────────────────────────────────────
Gives a deeper look at products, brands, inventory and order status.

  Product Distribution    : Donut chart of product count (SKU) by category
  Size-wise Inventory     : Column chart of inventory units by size
                            (XS, S, M, L, XL)
  Brand Performance       : Bar chart of revenue (Rs. Cr) by brand
  City Tier Analysis      : Column chart of revenue (Rs. Cr) by city tier
  Top Products by Revenue : Table with Product Name, Brand, Category,
                            Total Orders and Total Revenue
  Order Status            : Donut chart of Cancelled, Shipped, Returned
                            and Delivered orders

NAVIGATION
A left-hand navigation bar switches between Page 1 and Page 2.
Page 2 also has a "Back to Page 1" button.


──────────────────────────────────────────────────────────────
5. INTERACTIVITY
──────────────────────────────────────────────────────────────
  * All visuals on a page are linked to each other.
  * Selecting a value in a slicer updates the cards and charts.
  * Clicking a bar, column or donut slice cross-filters other visuals.
  * Cards and totals recalculate for the current selection.


──────────────────────────────────────────────────────────────
6. DATASET
──────────────────────────────────────────────────────────────
FILES USED

  1) myntra_orders_master.csv  (1,80,000 rows)
     Used for: orders, revenue, brand, category, city tier,
     order status and the product table.

  2) myntra_product_catalog.csv  (2,500 rows)
     Used for: product distribution and size-wise inventory.

FILES NOT USED (AND WHY)

  * myntra_festive_orders.csv, myntra_summer_orders.csv,
    myntra_winter_orders.csv
    These are subsets of the master file (their Order_IDs already
    exist in the master file). Loading them would double-count
    orders and revenue.

  * myntra_web_catalog.csv
    Contains only ratings and review counts, which are not part of
    this dashboard.


──────────────────────────────────────────────────────────────
7. DATA PREPARATION (POWER QUERY)
──────────────────────────────────────────────────────────────
  1. Brand_Name: removed extra spaces and standardised capitalisation
     (for example NIKE, " Nike" and Nike became Nike).
  2. Order_Date: converted the different date formats into one
     Date type.
  3. Data types: set correctly for date, whole number and decimal
     columns.
  4. Tables were renamed to Orders and Catalog.
  5. SizeData table: a small table holding total units for each size
     (XS, S, M, L, XL), used for the Size-wise Inventory chart.


──────────────────────────────────────────────────────────────
8. DATA MODEL
──────────────────────────────────────────────────────────────
  Catalog (SKU)  ──── One to Many ────>  Orders (SKU)

The relationship uses the SKU column with single-direction filtering.
SizeData is a standalone table used only for the size chart.


──────────────────────────────────────────────────────────────
9. DAX MEASURES
──────────────────────────────────────────────────────────────
  Total Orders    = DISTINCTCOUNT(Orders[Order_ID])
  Total Revenue   = SUM(Orders[Net_Revenue])
  Revenue Cr      = DIVIDE([Total Revenue], 10000000)
  Revenue Cr Text = "Rs. " & FORMAT([Revenue Cr], "0.00") & " Cr"
  Total Products  = DISTINCTCOUNT(Catalog[SKU])


──────────────────────────────────────────────────────────────
10. KEY OBSERVATIONS
──────────────────────────────────────────────────────────────
  * Overall: 180K orders and Rs. 118.90 Cr in revenue.
  * City Tier (orders): Tier 2 has the largest share (49.97%),
    followed by Tier 1 (37.46%) and Tier 3 (12.57%).
  * City Tier (revenue): Tier 2 leads with about Rs. 59.33 Cr, then
    Tier 1 (about Rs. 44.64 Cr) and Tier 3 (about Rs. 14.93 Cr).
  * Category: Kids Wear (23.9K) and School Shoes (21.8K) have the
    most orders; Handbags has the fewest (9.4K).
  * Brand (orders): Nike has the most orders, and the 10 brands are
    fairly close to each other.
  * Brand (revenue): Nike leads with about Rs. 13.32 Cr, followed by
    Puma and HRX.
  * Inventory: Size M has the highest inventory (about 0.50M units);
    XS and XL are the lowest (about 0.25M each).
  * Order Status: orders are split almost evenly across Cancelled,
    Shipped, Returned and Delivered (about 25% each).


──────────────────────────────────────────────────────────────
11. BUSINESS RECOMMENDATIONS
──────────────────────────────────────────────────────────────
  1. Focus marketing and delivery capacity on Tier 2 cities, which
     bring the highest share of orders and revenue.
  2. Keep higher stock of size M, which has the highest inventory
     and is the most common size.
  3. Cancelled and Returned orders together are about 50% of all
     orders. This is worth investigating to reduce losses.
  4. Promote Kids Wear and School Shoes, the top categories by
     orders, and review low-order categories such as Handbags.
  5. Brand revenue is fairly balanced, so offers can be planned
     brand by brand rather than relying on a single brand.


──────────────────────────────────────────────────────────────
12. DESIGN
──────────────────────────────────────────────────────────────
  * Dark navy header with the Myntra logo, page title and
    "Data as of" date.
  * Dark purple left navigation bar with page icons.
  * White cards with rounded borders on a light grey canvas.
  * Colour palette: purple, green, blue, orange, teal and navy.


──────────────────────────────────────────────────────────────
13. HOW TO USE
──────────────────────────────────────────────────────────────
  1. Open the .pbix file in Power BI Desktop.
  2. Use the slicers on Page 1 to filter by Brand, Category and
     City Tier.
  3. Click any chart element to cross-filter the rest of the page.
  4. Use the left navigation bar to move between Page 1 and Page 2.


──────────────────────────────────────────────────────────────
14. NOTES
──────────────────────────────────────────────────────────────
  * The dataset has an order status of "Shipped" (there is no
    "Pending" status), so Shipped is shown on the Order Status chart.
  * The category list in the data (for example Sneakers, School
    Shoes, Face Wash, Lipstick) is different from a typical fashion
    catalogue, so the charts show the real categories from the data.


──────────────────────────────────────────────────────────────
15. PROJECT HIGHLIGHTS & ACHIEVEMENTS
──────────────────────────────────────────────────────────────
  [x] Built a complete 2-page interactive dashboard in Power BI
  [x] Analysed 1,80,000 orders and 2,500 products
  [x] Created 14 interactive elements: 3 slicers, 2 KPI cards and
      9 charts / tables
  [x] Spotted that 3 seasonal files duplicated the master data and
      excluded them to avoid double counting
  [x] Cleaned inconsistent brand names and mixed date formats
  [x] Designed a custom branded layout with header, logo, navigation
      bar and page buttons
  [x] Connected two tables with a one-to-many relationship using SKU
  [x] Wrote DAX measures for orders, revenue and product counts
  [x] Turned the data into clear business recommendations


──────────────────────────────────────────────────────────────
16. SKILLS DEMONSTRATED
──────────────────────────────────────────────────────────────
  * Data Cleaning and Transformation (Power Query)
  * Data Modeling (relationships, one-to-many)
  * DAX (measures and calculations)
  * Data Visualisation (donut, column, bar, table, cards, slicers)
  * Dashboard Design and User Experience
  * Page Navigation and Interactivity
  * Business Analysis and Insight Writing


──────────────────────────────────────────────────────────────
17. FUTURE ENHANCEMENTS
──────────────────────────────────────────────────────────────
  * Add a date slicer and monthly trend charts
  * Add month-on-month and year-on-year growth indicators
  * Add drill-through pages for product-level details
  * Add a customer and delivery-time analysis page
  * Create a mobile-friendly layout
  * Publish the report to Power BI Service with scheduled refresh


──────────────────────────────────────────────────────────────
18. AUTHOR
──────────────────────────────────────────────────────────────
  Name          : [ Gupta Sneha ]
  Course / Class: [ Data Analysis ]
  Date          : 03/11/2026
  Email         : [ snehagupta47103@gmail.com ]


──────────────────────────────────────────────────────────────
19. ACKNOWLEDGEMENT
──────────────────────────────────────────────────────────────
I would like to thank my teacher for the guidance and for giving me
the opportunity to work on this project. It helped me learn how to
turn raw data into a clear and interactive dashboard.


══════════════════════════════════════════════════════════════
              Thank you for viewing this project!
══════════════════════════════════════════════════════════════
