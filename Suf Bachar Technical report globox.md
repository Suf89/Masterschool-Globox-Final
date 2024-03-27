# A/B Test Report: Food and Drink Banner

## Purpose

The goal of this AB test is to determine whether a specific change has a significant impact on conversion rate and average amount spent per user, compared between the two groups - test and control. 

## Hypotheses

Null Hypothesis (H0) - No significant difference in conversion rates & Avg money spend between treatment and control groups.
Alternative Hypothesis (H1): Treatment group has a significant impact on conversion rate average amount spent per user compared to the control group.

## Methodology

### Test Design

- **Population:** all users using the application - the website 

- **Duration:** start date : 25/1/23 , End Date : 6/2/23

- **Success Metrics:** 

we measure success by comparing the conversion rate and avg money spend between the two groups.

## Results
### Data Analysis
- **Pre-Processing Steps:** 

the pre-processing steps performed on the dataset includes cleaning and the data, deleting outliers etc & cleaning the data by using a few parameters such as Uid, user device, country, test group and wheter if the user were converted or not. 
we removed null values in beekeper before importing the dataset inside tableau.

```sql

SELECT u.id as user_id, 
			 u.country as user_country, 
       u.gender as gender, 
       g.device as ios_or_android, 
       CASE WHEN g.group = 'A' THEN 'Control Group' ELSE 'Treatment Group' END AS test_group,
			 SUM(COALESCE(a.spent, 0)) AS sum_money_spent,
       CASE WHEN a.spent IS NOT NULL then 1 ELSE 0 END as conv_or_not
FROM users AS u
LEFT JOIN groups AS g
 ON g.uid = u.id
LEFT JOIN activity AS a
	ON a.uid = u.id
GROUP BY user_id, user_country, gender, ios_or_android, test_group, conv_or_not
ORDER BY sum_money_spent DESC
;

```

- **Statistical Tests Used:**

we used both z-test & t-test :
Conversion Rate - used Z-test to check and compare for percentages difference.
Avg Money Spend - used T-test to check and compare for mean difference.



- **Results Overview:** 

based on conversion rate using the z-test we see a small change between the groups  (control group - 3.92% vs treatment group - 4.62%), a 0.71% increase (p value = 0.0001), suggests that the banner impacts positively. altough, using the t-test on the average money spend we can see no significant difference in numbers, The control group with average amount spent of $3.37, and  treatment group has an average amount spent of $3.39 (p value = 0.9439). the lack of difference results the concern wheter the increase of conversion translates to a higher revenue. therefore it is recommended to reject the alternative hypotesis and not to invest in the development of the new banner, being positively raising conversion rate showing no significant change in avg money spend.

### Findings

## Interpretation
- **Outcome of the Test(s):** the outcome of the test shows that there is no significant advantage to invest in the development on the new banner being positively raising conversion rate , but not showing significant change in avg money spend. 

- **Confidence Level:** State the statistical confidence
Conversion Rate - 95% Confidence Interval (0.0437, 0.0489)
Avg Money Spend - 95% Confidence Interval (-0.4386, 0.4713)


## Conclusions
- **Key Takeaways:** 

While the positive impact on conversion rates is promising, the lack of difference in average amount spent requires further investigation. 
an additional analyses and alternative launch strategies before making a final decision on launching the product seems to be required.

we learned that although there is a small increase in the conversion rates compared between the two groups there are more parameters that provides a new and different perspective on wether on not to develop a feature to increase overall revenue.
we need to think about multiple perspectives when conducting a comprehensive test to check for differences based on the business goals and measures - for example check for longer test period, work on bigger user base etc.


- **Limitations/Considerations:** 

based on our test the analysis shows that we need to test those parameters on a larger amout of users in order to see a bigger difference between the groups around 300k users (while the test group was formed by 24,343 users, and the treatment group was formed by 24,600).

## Recommendations
- **Next Steps:** 

1. Analyze click-through rates (CTRs): Did the banner increase the number of people who clicked 
2. Segment data: Analyze conversion rates and amount spent for different user segments. Were there specific groups who responded better to the new banner?
3. Track revenue and profitability: Monitor real-world data after launching the banner to see if the increased conversion actually translates to higher revenue and profitability.
4. Consider alternative launch strategies: Instead of a full launch, consider a gradual rollout to a smaller segment of users to learn more about its impact before wider deployment.

by my opinion based on the data we need to conduct the test for longer period of time for more than 2 weeks we can see a more bright change whether bigger or smaller and than decide wheter its worth the cost of developing this new feature.

- **Further Analysis:** 

based on the facts derived from the data it seems we need a lrger amount of sampling to compare the AB test and see a bigger difference in the numbers in order to choose to go with the new or improved version.

