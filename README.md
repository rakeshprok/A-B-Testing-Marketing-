# Project Report
**Title:** Evaluating Ad Effectiveness with A/B Testing — A Real-World Data Science Approach

In today’s digital world, companies spend a lot on ads — but how do we know if those ads actually work? That’s what this project set out to explore using A/B testing and basic statistics. We wanted to see if showing people a promotional ad would lead to more purchases compared to showing them a general message (called a PSA — public service announcement). To answer that, we used a real-world dataset from Kaggle and did some hands-on analysis using Python.

The dataset had thousands of users who were randomly assigned to one of two groups: one group saw an ad, and the other saw a PSA. We also had details like whether each user ended up buying something (conversion), how many ads they saw, and the day and time those ads appeared. After removing unnecessary columns like user IDs and checking for duplicates, we started analyzing the data.

**Raw Observation through EDA** :
1. Friday Sees Slightly Higher Engagement: Among all weekdays, Friday stands out with a conversion rate of ~15.7%, slightly ahead of other days. While not a dramatic lead, this could suggest users are more receptive toward the weekend.
2. 1 PM is Peak Ad Hour: The most frequent time slot for seeing ads is 1:00 PM, indicating a possible scheduling strategy or natural user activity peak. This could help in future ad timing optimization.
3. Ad Group Dominates Exposure : A majority of users (96%) were shown ads, while 4% received PSAs. Though unbalanced, this setup reflects a real-world scenario where ad campaigns often have broader reach.
4. Room for Growth in Conversions
With an overall conversion rate of 2.5%, there’s clear potential to optimize user engagement. This provides a great opportunity to identify what drives better performance.
We also found that users who converted (made a purchase) had typically seen more ads — around 25 on average — compared to non-converters, who had seen about 10. That points to something marketers already suspect: **repeated exposure (or remarketing) works**. But it’s not enough to just “see” the pattern — we needed to test if the difference was statistically real.

So, we used something called the **Chi-Square Test**, which checks if two categories (like ad type and conversion) are related or if the difference is just by chance. When we compared the Ad group vs. the PSA group, the test gave us a Chi-square value of 54.01 and a p-value of 1.99e-13 — which is way below the standard cutoff of 0.05. That means the result is **highly significant**, and we can confidently say that ads converted better than PSAs.

We ran similar Chi-Square tests for day of the week and hour of the day — and again, the results were very significant (p-values almost zero). So yes, the **day and time you show an ad can strongly influence conversion**.

Next, we wanted to test whether the number of ads seen made a difference. Since this was a numerical variable (not just categories), we first checked if the data was “normal” using a **Shapiro-Wilk test** — it wasn’t. Then we checked if the spread (variance) was equal between converters and non-converters using **Levene’s test** — again, it wasn’t. Because those assumptions failed, we used the **Mann-Whitney U test**, which is perfect for comparing two groups when the data is not normally distributed and variances are unequal. The Mann-Whitney test gave us a p-value of 0.0 — meaning the difference is highly significant. This confirmed that users who saw more ads were much more likely to convert.

These were the key statistical tests used in this project: **Chi-Square Test**, **Shapiro-Wilk Test**, **Levene’s Test**, and **Mann-Whitney U Test**. Together, they helped us carefully evaluate both categorical and numerical factors affecting conversion, while following all statistical assumptions step by step.

**Statistical Testing**
1. **Chi-Square Test** (for categorical comparisons)
This test helps check whether two categories are related — like ad type and conversion status.
Ad vs PSA: Conversion rate was significantly higher in the Ad group (p < 0.001)
Day of the week vs Conversion: Days like Friday showed slightly higher conversion (p ≈ 0.0)
Hour of day vs Conversion: Afternoon hours had better results (p ≈ 0.0)
These tests confirmed that both message type and timing have a strong influence on conversions.

2. **Shapiro-Wilk Test** (for normality)
This test checks if a numeric variable (like ad counts) follows a normal distribution.
Result: The data was not normally distributed — so we couldn’t use t-tests.

3. **Levene’s Test** (for equal variance)
This checks whether two groups have similar spread or variance.
Result: Variance was unequal between converters and non-converters.

**Notes** : 1. Saphiro (Normality test) : P-values are way below 0.05 → both groups are not normally distributed, avoiding t-test
2. levene (Variance equality: whether two or more groups have equal variances) : Variances are not equal → another reason to avoid t-test.
3. hence comes Mann-Whitney test : Used to check if there's a difference in the number of ads seen by: Users who converted, Users who did not convert...
means asking : Do users who converted tend to see more ads than those who didn’t? or I'm not saying exactly how many ads cause conversion — instead testing whether there's a pattern in ad exposure that correlates with conversion behavior.

5. **Mann-Whitney U Test** (non-parametric test for numeric data)
Since the data wasn’t normal and variances were unequal, I used this test instead of a t-test.
Compared: Number of ads seen by converters vs non-converters
Result: p-value = 0.0 → Highly significant difference
Conclusion: Users who converted consistently saw more ads

6. **Cliff’s Delta** (Effect Size)
EFFECT SIZE : p-values tell us whether a difference is statistically significant.don’t tell the size or importance of the difference. Even though the p-value is 0.0 (i.e., statistically significant), Still confirming: Is the difference meaningful in practice?

Simple example:
let, A = [3, 4]
B = [1, 2]
Comparisons:
3 > 1 , 3 > 2 , 4 > 1, 4 > 2
All 4 comparisons show Group A > Group B →
𝛿 = 4−0  / 2*2
=1.0
This means:
“Every value in Group A is greater than every value in Group B”
→ Very strong effect.
here, Positive δ → Group A (converted users) tends to see more ads
Negative δ → Group A tends to see fewer ads

here, Result: 0.71, which is considered a large effect size
Interpretation: Converted users didn’t just happen to see more ads — they saw a lot more, which strongly influenced their behavior

**CONCLUSION : Final Business Insights**
Based on the analysis, there’s a clear and statistically significant difference in ad exposure between users who converted and those who didn’t (p < 0.001). The Ad group also showed a higher conversion rate than the PSA group. With a large effect size (Cliff’s Delta ≈ 0.71), it’s clear that more frequent ad exposure is strongly linked to conversions. This gives us solid direction to optimize our ad strategy — especially around timing (for example : around 2pm, day : friday) and frequency — which aligns well with user activity. oving forward, I’d recommend increasing ad exposure slightly during these peak hours and testing different messaging or formats within that window to boost engagement and drive even better results.

So, what does all this mean? In simple terms: 
- Ads work better than PSAs for driving conversions.
- Timing matters — show ads on Mondays and during peak hours.
- Show ads more than once — repetition really helps.

These insights can help companies make smarter decisions. Instead of spending randomly on ads, they can schedule them at the best times and focus more on remarketing. What we’ve done here mirrors what big tech companies like Google or Meta do daily — test small changes, analyze results with statistics, and optimize based on data.

Through this project, I learned how A/B testing works in real life, how to use statistics to back up your observations, and most importantly, how to turn raw data into useful insights. It also taught me how powerful it is to **tell a clear story using data**, especially when backed by tests that anyone — even non-technical people — can understand. That’s what makes data science so impactful.
