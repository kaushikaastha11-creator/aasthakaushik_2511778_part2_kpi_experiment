## 🧹 Experiment Data Cleaning & Quality Log (Task 4)

A comprehensive data quality audit was conducted within `analysis/experiment_analysis.xlsx` to ensure statistical validity and prevent data skew before launching tests. Below is the documentation of those quality verification checks:

### 1. Duplicate Records Audit
* **Check Method:** Applied Excel's `Remove Duplicates` function and run a conditional formatting unique-value count on the `user_id` primary key column.
* **Findings:** 0 duplicate rows detected out of 1,400 user records.
* **Handling:** No deduplication actions were required.

### 2. Missing & Null Values Strategy
* **Check Method:** Profiled blank fields across all columns.
* **Findings:** Two columns contained blank values:
  * `days_to_convert`: Blank for 1,293 users.
  * `traffic_source`: Blank for various user lines.
* **Handling:** * Blanks in `days_to_convert` are expected logical behavior indicating non-converted users. Forcing a zero would heavily skew conversion velocity analytics. They are kept as nulls and omitted only during conditional average operations (`AVERAGEIF`).
  * Missing values in `traffic_source` are preserved as a baseline "Direct/Unclassified" segment rather than dropping rows.

### 3. Structural Integrity & Binary Values Validation
* **Check Method:** Validated data fields against their categorical criteria via column value sorting and unique filters.
* **Findings:** All core conversion funnel metrics (`visited_landing_page`, `started_trial`, `completed_onboarding`, `converted_to_paid`, `refund_requested`) conformed perfectly to a Boolean/Binary domain constraint (`0` or `1`).

### 4. Revenue Outlier Analysis
* **Check Method:** Calculated the distribution of `revenue_30d` using Tukey's fences method ($IQR \times 1.5$) among paid converters.
* **Findings:** Maximum entries near \$1,009.90 were identified as statistical outliers. However, a deep breakdown showed these anomalies are strictly tied to high-tier premium plans.
* **Handling:** Outliers were retained. Dropping them would artificiality deflate the True Treatment impact on total revenue performance.

### 5. Group Counts & Segment Distribution Balance
* **Check Method:** Evaluated sample sizes using a Pivot Table split across `experiment_group`, `region`, and `device_type`.
* **Findings:** The sample shows an exact $50/50$ structural split: **700 users in Control** and **700 users in Treatment**. Segment ratios match cleanly across both groups:
  * *Device Split:* Desktop, Mobile, and Tablet maintain an identical distribution profile between both testing variants, indicating proper random assignment.
