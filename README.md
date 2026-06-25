# Business Experimentation & KPI Analysis: New Onboarding Campaign

## 1. Business Context & Problem Statement
* **What decision needs to be made:** Leadership must decide whether to fully launch the new onboarding and activation campaign experience (Treatment group) to 100% of the user base, reject it completely, continue testing, or deploy it exclusively to high-performing user segments.
* **Who the decision impacts:** This decision directly impacts incoming trial/freemium users, product management team operations, and customer support resource allocation.
* **What metric should improve:** The primary target for improvement is the **Paid Conversion Rate** and early **User Engagement Score**.
* **What risks must be monitored (Guardrails):** Potential spikes in customer support ticket volumes (`support_tickets_30d`), an increase in post-conversion refund requests (`refund_requested`), or drops in mid-funnel conversion efficiency.
* **Evidence required for recommendation:** Statistically significant improvement in the North Star metric alongside stable or improved guardrail metrics, validated via a two-sample proportion test or t-test at a 95% confidence level ($\alpha = 0.05$).

---

## 2. North Star Metric Selection & Rationale
* **Selected North Star Metric:** **Paid Conversion Rate** (Users Converted to Paid / Total Signups)
* **Rationale:** As a subscription-based digital product, long-term ARR/MRR growth is heavily reliant on top-of-funnel efficiency. While early metrics like "Trial Start Rate" or "Onboarding Completion Rate" show product adoption, they do not guarantee monetization. 
* **Why supporting metrics aren't the North Star:** Metrics such as *Engagement Score* or *Onboarding Completion* are leading indicators, not lagging business outcomes. You cannot pay for infrastructure with unmonetized engagement.
* **Risks of blind optimization:** If we optimize solely for Paid Conversion Rate by aggressively gating features or using dark UX patterns, we might attract low-intent users who instantly request refunds or overwhelm support channels, causing a net-negative business impact.

---

## 3. KPI Tree Blueprint Summary
* **North Star:** Paid Conversion Rate
    * *Driver 1: Funnel Progression Rate*
        * Sub-driver: Landing Page Visit Rate
        * Sub-driver: Trial Activation Rate
    * *Driver 2: Product Adoption/Onboarding*
        * Sub-driver: Onboarding Completion Rate
        * Sub-driver: Average Engagement Score
    * *Driver 3: Monetization Velocity*
        * Sub-driver: Average Days to Convert
        * Sub-driver: Plan Type Tier Distribution
* **Guardrails Monitored:** 30-Day Refund Rate, Support Ticket Rate per User, Average Revenue Per Converted User (ARPPU).

---

## 4. Experiment Analysis & Data Prep Approach
During data cleaning within `analysis/experiment_analysis.xlsx`, the following steps were taken:
1.  **Duplicate Check:** Handled duplicate `user_id` values via Excel's *Remove Duplicates* feature.
2.  **Missing Value Treatment:** Filtered out rows missing critical assignment groups or structural tracking IDs. Blank values in `days_to_convert` were preserved as expected behaviors representing non-converted users.
3.  **Outlier Removal:** Isolated extreme `revenue_30d` value spikes using the IQR (Interquartile Range) method to ensure averages were not skewing the baseline.
4.  **Consistency Check:** Validated that binary variables (`started_trial`, `completed_onboarding`, `converted_to_paid`, `refund_requested`) only contained 0 or 1 values.

---

## 5. Summary of Results & Recommendation
* **Hypothesis Testing:** Conducted a two-proportion Z-test comparing the Paid Conversion Rates of Control vs. Treatment.
* **Final Decision:** *[Insert your final action based on your sheet results, e.g., Full Launch / Segmented Launch / Reject]*
* **Detailed Documentation:** See `outputs/recommendation_memo.md` and `analysis/hypothesis_test_notes.md`.
