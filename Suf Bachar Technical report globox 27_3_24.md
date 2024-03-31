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

in short - Promising Start, Needs More Data

Conversion rates are up, which is a positive sign for the new feature. However, the average purchase amount didn't shown a significant increase.

in a deep diving in the data : 

1. Limited Sample Size: Our test group wasn't large enough (24,343 users) to detect a definitive impact on revenue. We recommend expanding the test to around 300,000 users.
Test Duration: Two weeks might not be enough to capture the full impact. Extending the test period will provide a clearer picture.
User Segmentation: Analyzing different user groups (e.g., location, demographics) might reveal variations in response to the feature.
Next Steps:

2. Analyze click-through rates: Did the new feature grab user attention?
Segment user data: See which groups responded best to the feature in terms of conversion and average spend.
Track revenue and profitability: Does the conversion increase translate to higher profits?
Consider a gradual rollout: A phased launch can provide valuable insights before full deployment.
Recommendation:

3. Extend the test: Gather more data over a longer period.
Segment user data: Tailor the app experience for different user groups.
Evaluate alternative launch strategies: Consider a phased rollout for a controlled launch.
By taking these steps, we'll gain a more comprehensive understanding of the feature's impact and make a data-driven decision about its future.

