# Engagement Analysis between TikTok and Instagram 
----
## **Datasets**

>[TikTok User Profiles Dataset](https://www.kaggle.com/datasets/manishkumar7432698/tiktok-profiles-data)
>
>[Top 200 Instagram Influencers Data (Cleaned)](https://www.kaggle.com/datasets/syedjaferk/top-200-instagrammers-data-cleaned)

----
## Objective
>To understand the relationship between the number of followers and the engagement rate of influencers on TikTok and Instagram.
>
>This analysis aims to provide insights into which platform offers the best engagement relative to its follower count, which can be invaluable for businesses looking to maximize their marketing efforts.

----

## Steps Taken

>### 1. Data Acquisition
>
>Datasets for influencers on TikTok and Instagram were sourced from Kaggle. These datasets provide information on the top influencers, their follower counts, and their engagement rates.
>
>### 2. Data Preparation
>
>The datasets were loaded into SQL tables for further analysis. Basic data cleaning was performed to handle missing values and outliers.
>
>### 3. Data Analysis
>
>SQL was used to calculate the average engagement rate for each platform and the correlation between followers and engagement rate for each platform.
>
>This SQL code unions the average engagement rates from the three tables (one for each platform) and labels them with the respective platform name.

```sql
-- SQL code to calculate average engagement rate for each platform
SELECT 'TikTok' as Platform, AVG(engagement_rate) as Average_Engagement
FROM tiktok_data
UNION
SELECT 'Instagram', AVG(engagement_rate)
FROM instagram_data;
```
>This SQL code unions the correlation coefficients between followers and engagement rates from the three tables and labels them with the respective platform name.

```sql
-- SQL code to calculate correlation between followers and engagement rate for each platform
SELECT 'TikTok' as Platform, CORR(followers, engagement_rate) as Correlation
FROM tiktok_data
UNION
SELECT 'Instagram', CORR(followers, engagement_rate)
FROM instagram_data;
```
> These SQL codes are used to determine how closely related the number of followers is to the engagement rate for influencers on TikTok and Instagram.
> 
> If the correlation is close to 1, it means that as the number of followers increases, the engagement rate also tends to increase, and vice versa if the correlation is close to -1.
> 
> If the correlation is close to 0, it indicates that there's no significant relationship between the two variables. 

```sql
-- SQL code to calculate correlation between followers and engagement rate for TikTok
SELECT 'TikTok' as Platform, CORR(followers, engagement_rate) as Correlation
FROM tiktok_data;
```
```sql
-- SQL code to calculate correlation between followers and engagement rate for Instagram
SELECT 'Instagram', CORR(followers, engagement_rate)
FROM instagram_data;
```
----
## **Assumptions**

>#### Engagement Rate is a Reliable Metric:
>We assume that the engagement rate provided in the datasets is a reliable metric for measuring the actual engagement of followers with the influencer's content. This is based on the common industry practice of using engagement rate as a key performance indicator.
>
>#### Data Completeness:
>We assume that the datasets provide a comprehensive list of top influencers for each platform. This is to ensure that our analysis is representative of the actual influencer landscape on these platforms.
----
## **Visualizations**

>Top 10 Influencers by Followers for Each Platform

![Top 10 TikTok Accounts by Followers](https://chat.noteable.io/origami/o/8de8050bdaa94b0e8694271d1b48fffd.png)
```python
import pandas as pd
import matplotlib.pyplot as plt

# Load the TikTok dataset
tiktok_data = pd.read_csv('TikTok profiles dataset (Public web data).csv')

# Filter the top 10 influencers by followers
top_10_tiktok = tiktok_data.nlargest(10, 'Followers')

# Plotting the data
plt.figure(figsize=(12, 8))
plt.barh(top_10_tiktok['Name'], top_10_tiktok['Followers'], color='blue')
plt.xlabel('Number of Followers')
plt.ylabel('Influencer Name')
plt.title('Top 10 TikTok Influencers by Followers')
plt.gca().invert_yaxis()
plt.show()
```

![Top 10 Instagram Accounts by Followers](https://chat.noteable.io/origami/o/cb1f382189924b49b8036354c8690319.png)
```python
# Load the Instagram dataset
instagram_data = pd.read_csv('top_200_instagrammers.csv')

# Filter the top 10 influencers by followers
top_10_instagram = instagram_data.nlargest(10, 'Followers')

# Plotting the data
plt.figure(figsize=(12, 8))
plt.barh(top_10_instagram['Name'], top_10_instagram['Followers'], color='purple')
plt.xlabel('Number of Followers')
plt.ylabel('Influencer Name')
plt.title('Top 10 Instagram Influencers by Followers')
plt.gca().invert_yaxis()
plt.show()
```

>Correlation between Followers and Engagement Rate by Platform

![Correlation between Followers and Engagement Rate by Platform](https://chat.noteable.io/origami/o/aa0f7f4dd9d949c5aa978943df89cae8.png)
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the datasets
tiktok_data = pd.read_csv('TikTok profiles dataset (Public web data).csv')
instagram_data = pd.read_csv('top_200_instagrammers.csv')

# Calculate the correlation between followers and engagement rate for TikTok and Instagram
tiktok_corr = tiktok_data['followers'].corr(tiktok_data['engagement_rate'])
instagram_corr = instagram_data['followers'].corr(instagram_data['engagement_rate'])

# Create a DataFrame to store the correlation values
correlation_data = pd.DataFrame({
    'Platform': ['TikTok', 'Instagram'],
    'Correlation': [tiktok_corr, instagram_corr]
})

# Plot the data
plt.figure(figsize=(10, 6))
sns.barplot(x='Platform', y='Correlation', data=correlation_data, palette='viridis')
plt.title('Correlation between Followers and Engagement Rate by Platform')
plt.ylabel('Correlation Coefficient')
plt.xlabel('Platform')
plt.show()
```
----
## **Conclusion**

>The analysis reveals that TikTok influencers tend to have a higher average engagement rate compared to Instagram influencers.
>
>However, the correlation between the number of followers and engagement rate is stronger on Instagram than on TikTok.
>
>This suggests that while TikTok might offer a broader reach and higher engagement on average, the relationship between followers and engagement is more consistent on Instagram.
>
>Businesses should consider these insights when deciding on which platform to focus their marketing efforts, depending on whether they prioritize reach, average engagement, or the consistency of engagement relative to follower count.
----
## **Further Considerations**

>This analysis can be further expanded by considering additional metrics such as the type of content posted, the frequency of posts, and the demographics of the followers.
>
>Such an expanded analysis can provide a more holistic view of the influencer landscape and offer more nuanced insights for businesses.
----
## **Contact**

> I'm always open to discussing data analytics, project collaborations, or any other opportunities. Feel free to reach out to me through any of the channels below:
>
> LinkedIn: [Wendy Liang](https://www.linkedin.com/in/wendyliang38/)
>
> Email: wendybliang38@gmail.com
>
> Portfolio: [GitHub](https://github.com/wendifultimes/wendy-liang)
>
> If you have any questions or feedback regarding this project, please don't hesitate to open an issue or submit a pull request.
