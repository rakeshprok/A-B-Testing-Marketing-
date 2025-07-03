# Project Report
**Title:** Evaluating Ad Effectiveness with A/B Testing — A Real-World Data Science Approach

In today’s digital world, companies spend a lot on ads — but how do we know if those ads actually work? That’s what this project set out to explore using A/B testing and basic statistics. We wanted to see if showing people a promotional ad would lead to more purchases compared to showing them a general message (called a PSA — public service announcement). To answer that, we used a real-world dataset from Kaggle and did some hands-on analysis using Python.

The dataset had thousands of users who were randomly assigned to one of two groups: one group saw an ad, and the other saw a PSA. We also had details like whether each user ended up buying something (conversion), how many ads they saw, and the day and time those ads appeared. After removing unnecessary columns like user IDs and checking for duplicates, we started analyzing the data.

Right away, we noticed that most users (96%) had seen ads, and only a small group (4%) had seen PSAs. Out of everyone, only about 2.5% actually bought the product — so the conversion rate was low overall. But when we dug deeper, patterns started to show. For example, conversions were noticeably higher on Mondays, especially between 4 PM and 8 PM — which makes sense because people are often more active online during lunch or in the evening.

We also found that users who converted (made a purchase) had typically seen more ads — around 25 on average — compared to non-converters, who had seen about 10. That points to something marketers already suspect: **repeated exposure (or remarketing) works**. But it’s not enough to just “see” the pattern — we needed to test if the difference was statistically real.

So, we used something called the **Chi-Square Test**, which checks if two categories (like ad type and conversion) are related or if the difference is just by chance. When we compared the Ad group vs. the PSA group, the test gave us a Chi-square value of 54.01 and a p-value of 1.99e-13 — which is way below the standard cutoff of 0.05. That means the result is **highly significant**, and we can confidently say that ads converted better than PSAs.

We ran similar Chi-Square tests for day of the week and hour of the day — and again, the results were very significant (p-values almost zero). So yes, the **day and time you show an ad can strongly influence conversion**.

Next, we wanted to test whether the number of ads seen made a difference. Since this was a numerical variable (not just categories), we first checked if the data was “normal” using a **Shapiro-Wilk test** — it wasn’t. Then we checked if the spread (variance) was equal between converters and non-converters using **Levene’s test** — again, it wasn’t. Because those assumptions failed, we used the **Mann-Whitney U test**, which is perfect for comparing two groups when the data is not normally distributed and variances are unequal. The Mann-Whitney test gave us a p-value of 0.0 — meaning the difference is highly significant. This confirmed that users who saw more ads were much more likely to convert.

These were the key statistical tests used in this project: **Chi-Square Test**, **Shapiro-Wilk Test**, **Levene’s Test**, and **Mann-Whitney U Test**. Together, they helped us carefully evaluate both categorical and numerical factors affecting conversion, while following all statistical assumptions step by step.

So, what does all this mean? In simple terms: 
- Ads work better than PSAs for driving conversions.
- Timing matters — show ads on Mondays and during peak hours.
- Show ads more than once — repetition really helps.

These insights can help companies make smarter decisions. Instead of spending randomly on ads, they can schedule them at the best times and focus more on remarketing. What we’ve done here mirrors what big tech companies like Google or Meta do daily — test small changes, analyze results with statistics, and optimize based on data.

Through this project, I learned how A/B testing works in real life, how to use statistics to back up your observations, and most importantly, how to turn raw data into useful insights. It also taught me how powerful it is to **tell a clear story using data**, especially when backed by tests that anyone — even non-technical people — can understand. That’s what makes data science so impactful.
