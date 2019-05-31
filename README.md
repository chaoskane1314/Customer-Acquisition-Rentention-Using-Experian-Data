# Customer-Acquisition-Rentention-Using-Experian-Data
### Kane Ren
<img src="image/experian.png">

### Background and the Data

Business can purchase data from Experian to get more insight about their customers.
<br>
By sending customer information to Experian and pay a fee. It will return back data of the customer in many area, such as their hobby, interest, etc.

My final data contain customers' subscription status and the customer's data from Experian.
<br>
Subscription Status is base on after a free trial subscription.
<br>
Active: users continue to subscribe after trial.<br>
Cancel/Expire: users op out of the subscription after trial.
### Goal
To find out if there is difference between customers that are still subscribing(Active group) vs customers that cancel(Cancel group) base on these data.

E.g.: if the "Active customers" had a significant higher or lower "Play Golf Value" than the "Cancel customers". Then this information can be use to target better customers, result in higher conversion on new customer acquisition or better retention on existing customers.

## Data and Cleaning
- The Data contain 20000 rows.
- For the categorical data, most column has 15745 rows of non-null data.
- For the numerical data,  most column has 17052 non-null data.
- a heatmap of missing data is shown below:

<img src="image/missing data.png">

When a data is missing in the categorical or numerical, the whole row of data seems to missing as well. I decide to split the data respectively, drop all the missing value because a whole row of missing value doesn't contribute anything to my analysis.

For this project, I will be only working on the numerical columns.

### Exploratory Data Analysis(EDA)
I will be plotting the distribution of both active group and cacel group on the same graph to see the the difference between the two.

By looking at the plot below, a better idea how the distribution for one column of numerical data looks like for each of the group. It will proivde information on what the is the shape, where the mean it is, and a general idea of the difference.

<img src="image/ wine lovers.png">

For the "wine lovers" column, both group has a positive skew distribution, with mode around 10, and the mean is 34.5 for the active user group, 39.55 for the cancel group.

Another two example: column "video gamer" and "dog owner".

<img src="image/video gamer.png">
<img src="image/ dog owners.png">

From the above two plot, both group actually has similar shape of distribution.<br>
However, for "video gamer" column, the mean is far more apart then the "dog owners" column.

### Correlation between numerical variable.
Check to see if there is any correlation between the data column. By doing this, if a model is need to be build upon the data, some collinearity relationship can be spot here.

To do so, a correlation heat map is created to identify these relationship.

<img align="center" src="image/corr heatmap.png">

Looking at the correlation heatmap above, we can definitely see some variable with strong correlation.

For example, the "medical policy" and "life insurance policy" has a correlation of 0.91. Its scatter plot shown below:

<p align="center">
<img src="image/sample scatter.png">
</p>

From the above scatterplot, we can see a strong pattern. As one variable increase, the other tend to increase as well.
<BR>
This make sense, since both medical and life insurance usually come together.

We can use the same technique to examine other pairs with high correlation as well. This might reduce the effect of collinearity for a better model fit in the future.

## Hypothesis Testing

Since the goal is to find out if there is really a difference between the score of Active group and Cancel group. I will be doing a  significance test on the difference of mean value. I will perform the test on two column here, but it can apply to all. Since the sample size is really large in this data,8700 for the active group and 8596 for the cancel group. I will use z-test instead of t-test since there will be nearly no difference in the result.

<p align="center">
<img src="image/null and alt.png">
</p>

The alpha for the z-test will be 0.02.

The two column to perform the test below will be the "wine lover" and "dog owners" columns

For "wine lover" column, looking at the shape of distribution,a highly positive skew is observed, I will perform a square root transformation on the data, the result will display below.<BR>
<p align="center">
Before:
<img src="image/ wine lovers.png">
After:
<img src="image/data transform.png">
</p>

The shape of the data really close to symmetric after the transformation, so we can approximate the data with a normal distribution.

Using the z-test to see if mean score of wine lover score differ between the Active and Cancel group yields:

Result of z = -12.196, p-value = 0.0000

- Conclusion, at alpha=0.02, a p-value of 0.0000 means we reject the null hypothesis test, it's really likely there is a difference between the mean wine lover score between the active group and cancel group.

Apply the same treatment for the dog owner column.
<BR>
Since the distribution of the data is already symmetric, transformation of data is not needed.

For the dog owner column, we get a result of z = 1.132, p-value = 0.1288.

<img src="image/Test.png">

- At alpha=0.02, a p-value of 0.1288 means we fail to reject the null hypothesis test, we can't say there is a difference between the mean dog owner score between the active and cancel group.

### Confidence interval
In the above significance test, we conclude there is a high possibility of difference in mean wine lover score between the two group. <BR>

But most of the time it is better to provide a confidence interval, the confidence interval provide more context on how much actually the difference is.

Creating a 95% Confidence Interval for the "wine lover" column yields: (-0.5099, -0.3687)

Since this is a square root of the data, the range will be from 1 to 10 (Original numerical column is 1 to 99)

Interpretation of this confidence interval:
- At a scale of 10, we are 95% confidence that the true mean difference of wine lover value between the active group and cancel group is between (-0.5099, -0.3687). In context, the lower the value, the more likely the person is a "Wine Lover", so the active group is more likely to be a wine person.

## Future Work
- Split into subgroups depend on type of subscription.
- Examine all data provide by Experian.
- Create a prediction model.
