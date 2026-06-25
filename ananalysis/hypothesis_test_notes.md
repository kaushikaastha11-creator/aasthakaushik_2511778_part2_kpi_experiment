# Statistical Hypothesis Testing Notes

## 1. Test Configuration
* **Metric Being Tested:** Paid Conversion Rate (Converted Users / Total Users in Group)
* **Reason for Choice:** This metric bridges initial customer acquisition with direct business monetization. It directly tests if the new onboarding flow successfully drives a customer's willingness to pay.
* **Significance Level ($\alpha$):** 0.05 (95% Confidence Level)
* **Tail Type:** Two-tailed test (to catch both unexpected significant negative performance or positive drops).

## 2. Hypothesis Formulation
* **Null Hypothesis ($H_0$):** $P_{\text{treatment}} = P_{\text{control}}$ 
    *(The new onboarding campaign has no statistical effect on the Paid Conversion Rate.)*
* **Alternative Hypothesis ($H_1$):** $P_{\text{treatment}} \neq P_{\text{control}}$
    *(The new onboarding campaign causes a statistically significant difference in the Paid Conversion Rate.)*

## 3. Mathematical Execution Framework
For a two-proportion z-test, the pooled proportion ($p_p$) and the test statistic ($z$) are computed using:

$$p_p = \frac{x_c + xt}{n_c + nt}$$

$$z = \frac{\hat{p}_t - \hat{p}_c}{\sqrt{p_p (1 - p_p) \left(\frac{1}{n_c} + \frac{1}{n_t}\right)}}$$

Where:
* $x_c, x_t$ = Total conversions in Control and Treatment respectively.
* $n_c, n_t$ = Total sample sizes for Control and Treatment respectively.
* $\hat{p}_c, \hat{p}_t$ = Calculated sample proportions.

## 4. Decision Rule & Interpretation Logic
* If **P-value $\le$ 0.05** (or calculated $|Z| > 1.96$): Reject $H_0$. Conclude that the onboarding changes caused a statistically significant shift in user behavior.
* If **P-value > 0.05**: Fail to reject $H_0$. Any observed absolute differences are likely caused by random sampling variance.
