# Ecommerce Returns and Refunds Analysis
An e-commerce Power BI project built to answer one question the business kept running into: the company sees returns happening, but can't explain them fast enough. This dashboard moves the conversation from "returns happened" to "why returns happened and what to fix first."

# Client Problem

Problem	: Detail

-> Refund leakage :	Money is leaving through refunds, but the exact category, reason, or channel behind it can't be isolated

-> Messy return reasons	: Return reasons arrive from multiple channels and need clean grouping before analysis

-> Hidden root causes	: Category-level charts hide the real issue — it lives in subcategory × return-reason combinations

-> Discount risk	: Heavy discounts may create low-intent purchases and increase return probability

# Dashboard Structure

Page 1 — Executive Summary

High-level return performance and refund pressure.

-> KPI cards : Total Orders (3,100), Returned Orders (745), Return Rate % (24.03%), Refund Amount (₹3.82M) — each with a MoM indicator

-> Monthly Return Trend — returned orders and refund amount over time, to catch spikes and seasonality

-> Return Reason Pareto — ranks return reasons against cumulative returned units to isolate the vital few causes

-> Returns by Category — which categories contribute the most returned units

-> Returns by Sales Channel — donut share of returned units across Mobile App, Marketplace, Website, and Offline Store

-> Slicers: Date Range • Category • Sales Channel • Reset Filters

<img width="538" height="335" alt="Screenshot 2026-08-13 190143" src="https://github.com/user-attachments/assets/5443b072-faa0-4b76-96a6-1cc746b419f3" />

Page 2 — Product Diagnostics

Root-cause page, intentionally without a Top 10 Returned Products visual.

-> KPI cards : Average Return Days (14.88), Products Returned (unique product count), Top Category (by returned units), Top Reason (by returned units)

-> Subcategory × Return Reason Heatmap — colour-intensity matrix exposing exact root-cause clusters

-> Avg Discount vs. Return Rate % scatter — tests whether heavier discounting correlates with higher return rates, bubbles coloured by risk level

-> Product Return Details table — product, subcategory, orders, returned units, return rate, refund amount, avg return days, avg discount %

-> Slicers: Date Range • Category • Sales Channel • Return Reason • Reset Filters

<img width="539" height="337" alt="Screenshot 2026-08-13 190211" src="https://github.com/user-attachments/assets/ec809907-709c-41be-b8e3-4e4d8a899b38" />

# KPI Glossary

<img width="886" height="183" alt="Screenshot 2026-08-14 131822" src="https://github.com/user-attachments/assets/dff5aa89-ca0c-4386-aa5d-5308f2082ea7" />

# Key Insights

-> Return Rate sits at 24.03%, up 5.24% MoM, with Returned Orders growing faster (+20.75% MoM) than Total Orders (+14.73% MoM) — return exposure is outpacing order growth, not just tracking it.

-> Refund Amount (₹3.82M) grew 15.84% MoM, and the monthly trend shows a sharp climb into Q4 (Nov–Dec), suggesting a seasonal or promotional driver worth isolating.

-> Just three reasons — Product Not As Expected, Wrong Size, and Damaged Product — account for 56.51% of all returned units, the clearest Pareto-style priority list for the business to act on first.

-> Fashion and Electronics are the two heaviest-returning categories by both total orders and returned units, with Fashion also holding the top spot on Page 2's diagnostics.

-> Mobile App is the largest source of returned units by channel, ahead of Marketplace, Website, and Offline Store.

-> Average Return Days is 14.88 and rose 22.93% MoM — customers are taking meaningfully longer to initiate returns, worth checking against any policy or fulfillment changes.

-> Men's Clothing paired with Wrong Size is the single darkest cell in the subcategory × reason heatmap — a concrete sizing-guidance gap rather than a general "returns are up" problem.

-> The discount-vs-return scatter shows a rough upward drift — several high-discount products cluster above the 20% return-rate benchmark line, supporting the discount-risk hypothesis from the problem statement.

# Business Recommendations

Root Cause : Recommended Action

-> Product Not As Expected : Improve product images, descriptions, and expectation-setting copy

-> Wrong Size : Add size guidance and a return-feedback loop for fashion and footwear

-> Damaged Product : Audit packaging and marketplace handling quality

-> Quality Issue : Build vendor scorecards using returned units and refund amount

-> Discount Risk : Avoid deep discounts on products already showing high return risk

# Data Model

Classic star schema built from a raw order-line grain (one row = one product line inside an order).

<img width="593" height="314" alt="Screenshot 2026-08-13 190249" src="https://github.com/user-attachments/assets/15221b5e-46df-4d8f-934d-b05e44bc6217" />

-> Fact_Orders — Brand, Customer_ID, Order_ID, Order_Date, Delivery_Date, Product_ID, Payment_Method, Discount_Pct, Product_Rating

-> Dim_Product — Brand, Category, Subcategory, Product_ID, Product_Name

-> Dim_Customers — Customer_ID, Customer_City, Customer_State, Customer_Segment

-> Dim_Channel — Sales_Channel

-> Dim_PaymentMethod — Payment_Method

-> Dim_ReturnReason — Return_Reason

-> Dim_Date — Date, Day_Name, Day_Number, Month_Name, Month_Number

All dimensions relate to Fact_Orders on a 1-to-many basis. Derived fields — Refund Amount, Return Days, Return Rate %, MoM deltas, and Pareto cumulative % — are all calculated in Power BI/DAX rather than sourced from the raw data.

# Tools & Techniques

-> Power BI Desktop — star-schema data modeling, DAX measures, Power Query cleaning

-> DAX — Return Rate %, Refund Amount, Average Return Days, MoM deltas, Pareto cumulative %, TOPN dynamic-text measures

-> Visuals used — KPI cards with MoM arrows, area/line trend chart, Pareto (column + cumulative line) chart, horizontal bar comparison, donut chart, matrix heatmap, scatter plot with risk colouring, detail table

# Repository Contents

├── README.md

├── screenshots/

│   ├── 01_executive_summary.png

│   ├── 02_product_diagnostics.png

│   └── 03_data_model.png

├── Return_Refund_Analysis.pbix       (Power BI report file)

└── data/                             (source/synthetic dataset, if shared)

# How to Use

1. Clone the repo and open Return_Refund_Analysis.pbix in Power BI Desktop.

2. On Page 1, use the Date Range, Category, and Sales Channel slicers (or the channel buttons at the top) to filter executive KPIs and charts.

3. Move to Page 2 for root-cause detail — filter further with the Return Reason slicer, then read the heatmap and scatter plot together to spot subcategory-level risk.

4. Use Reset Filters on either page to return to the full-year, all-channel view.

# About This Project

Built as a portfolio project to demonstrate diagnostic e-commerce BI: a raw order-line table modeled into a star schema, DAX-derived KPIs framed around explicit business decisions (not just numbers), and a two-page structure that moves a stakeholder from "what happened" to "what to fix first."
