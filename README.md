# Olist E-Commerce Logistics Optimization
> **HVIA Data & AI Solutions — Trial Training Task**  
> *End-to-End Data Pipeline, Governance Profiling, Root Cause Analysis (RCA).*

---

## Executive Summary
This repository presents an end-to-end analytical study and AI strategy framework designed for **Olist**, Brazil’s leading e-commerce marketplace integrator. Using **93,193 clean completed order transactions**, this project evaluates first-mile and middle-mile logistics bottlenecks, establishes rigorous data governance standards, and proposes a targeted 3-tier Data & AI solution roadmap to minimize delivery delays and align customer expectations.

---

## Key Findings & Quantified Impact
* **Platform Defect Rate:** Identified **7,101 late orders** out of 93,193 valid shipments (**7.62% overall late delivery rate**).
* **The 50/50 Root Cause Split:**
  * 🔴 **Seller SLA Failures (49.4% / 3,508 Orders):** First-mile handling delay where sellers exceed the standard 3-day dispatch SLA window.
  * 🟠 **Carrier & Route Inefficiencies (50.6% / 3,593 Orders):** Transit latency concentrated in long-haul regional freight corridors.
* **Geospatial Disparity:** Long-haul routes originating from **São Paulo (`SP`)** to Northeastern states suffer severe delay rates:
  * `SP ➔ AL` (Alagoas): **20.78% Late Rate** | **19.68 Avg Transit Days**
  * `SP ➔ MA` (Maranhão): **20.43% Late Rate** | **17.65 Avg Transit Days**
  * `SP ➔ BA` (Bahia): **12.87% Late Rate** | **15.48 Avg Transit Days**

---

## Data Governance & Pipeline Methodology
Before modeling, the raw dataset (~99k rows) underwent a structured **Data Governance & Profiling Audit**:

1. **Validity & Outlier Filtering:**
   * Removed log anomalies where dispatch timestamps preceded order approval dates.
   * Filtered extreme long-tail outliers (handling times > 100 days).
2. **Master Data Management (MDM) & Uniqueness:**
   * Verified $100\%$ uniqueness on Primary Keys (`order_id`, `customer_id`) to prevent entity duplication.
3. **Nullity Profiling (SQL Logic):**
   * Applied `AVG(CASE WHEN ...)` profiling to verify that non-random missing timestamps strictly correlated with `canceled` or `in_voiced` orders rather than ETL logging faults.

---
