
![youtube](https://user-images.githubusercontent.com/70446836/98875791-ed290380-244a-11eb-9883-2486d9b81acc.png)
# Youtube Trends
**Team Members:** Desiree Herschberger, William Pappas, Thomas Keane, Tas Nahar, Redeat Bekele, Sveena Sharma
# Motivation
  YouTube is a gigantic video-sharing platform based in San Bruno, California that earned a revenue of $15 billion in 2019. Due to the vast number of published videos, it is difficult to understand which categories, channels, or videos themselves are the most popular over time. It would seem reasonable that stakeholders in YouTube would like to understand what is trending and how their users interact with these videos. Is there a connection between the number of views, likes, dislikes, and comments on a given video? Is there a reason that certain video categories perform signifcantly better than other categories? Is it possible to predict user behavior over time? If these factors are known, it would be benefical for not only the executives/stakeholders, but the creators themselves to be able to predict success or failure.
  This repository consists of analysis performed on various YouTube datasets and includes observable trends. The data includes the Top US Trending Videos from Kaggle for August to November of 2020. It also includes three datasets from YouTube API: YouTube Search Items, YouTube Video Statistics, and Youtube Channel Statistics. This repository includes trend analysis on user behavior, video statistics, channel statistics, and category statisics from 2019 and 2020. It also provides insights during the strict Covid Lockdown in the US from March to June 2020.
  Hypotheses:
  - Societal events will align with YouTube Trends (ex. quarantine challenges/vlogs, new music video releases, video games etc.)
  - If viewer count increases, viewer reactions will increase as well. This includes number of likes and dislikes as well as number of comments.
  - Compared to 2019, YouTube viewer habits will differ in 2020 due to the pandemic. 
  - However, the lockdown will not affect the viewer trends themselves asthey will remain consistant regardless social circumstances.

Please review the following links to review the final data analysis and data exploration/clean-up process:
[MainPy](https://github.com/redeat17/Project-1/blob/master/YouTube_Trend_Analysis%20.ipynb)

# Table of Contents
[Questions Addressed](https://github.com/SVEENASHARMA/PythonProject#questions-addressed)
[Data Sources](https://github.com/SVEENASHARMA/PythonProject#data-sources)
[Data Cleaning and Exploration](https://github.com/SVEENASHARMA/PythonProject#data-cleaning-and-exploration)
[Summary Statistics](https://github.com/SVEENASHARMA/PythonProject#summary-statistics)
- Top Five Liked Videos from August to November 2020
- Most Published Videos per Category from August to November 2020
- Top Trending Channels from August to October 2020
- Relationship between View Count and Reactions per Category
- Comparison Between the Top Two Categories: Music vs. Entertainment
- Most Watched Videos in 2019
- Most Watched Videos in 2020
- The Most Viewed Quarantine Challenge Videos During Strict COVID Lockdown
[Findings and Observations](https://github.com/SVEENASHARMA/PythonProject#findings-and-observations)
[Post - Mortem](https://github.com/SVEENASHARMA/PythonProject#post---mortem)
# Questions Addressed
1) Why were certain categories trending during specific times?
2) Is there a relationship between certain user behaviors: View Count, # of Likes, # Dislikes, # Comments
3) Is there a difference in viewing habits from 2019 to 2020? Did the strict COVID lockdown in early 2020 impact viewer trends?
# Data Sources
This project used a Kaggle CSV file and YouTube API to create the datasets regarding trends overtime based on the number of views. The CSV file soley focuses on US Trending data whereas the YouTube API expanded internationally. The data collected was transformed in order to analyze and visualize with Python; it included the following factors:
- Video Title
- Channel Title
- Publish Time
- Tags
- Views
- Likes and Dislikes
- Description
- Comment Count
The following three datasets were pulled from the YouTube API: YouTube Search Items, YouTube Video Statistics, and Youtube Channel Statistics. All three datasets are linked by the unique Video ID and Channel ID fields.





# Data Cleaning and Exploration
**Pandas Process**
With Pandas, we read the CSV file and parsed the YouTube date format into a datetime format. We calculated the lag time for each video to trend and replaced the category ID numbers with category names for readability. Afterwards, we sorted the dataframe by the number of likes and dropped any duplicate columns. We also used the groupby function in various cells for the date, number of published trending videos, categories, and months.

**Matplotlib Process**
Using the previously created PANDAS dataframe we created additional layers to parse specific data per month, this included trending categories and user statistics. We also added supplemental grouby functions to organize this data. Once the data was organized, we were able to create bar and scatter graphs using pyplot. The heatmap was created with a correlation function and seaborn.

**API Process**
The dataset includes data gathered from videos on YouTube API that contained highest viewcounts in specific time periods. There are three kinds of data files, the first one includes youtube search items with snippet descriptions, the second includes youtube video statistics, and the third includes youtube channel statistic. They are all linked by the unique video_id and channel_id field. Once we pulled the necessary data, we dropped the duplicate or irrelevant columns and reorganized the created dataframes for readability. We also merged data frames based on the video ID and channel ID fields. This dataset was sorted based on view count, number of likes and dislikes. One issue that arose while exploring the data is that we had to repeatedly call the API without going over the quota. There are only so many requests we could do and we had to implement another method that allowed us to continue our analysis without overextending our API limit.

**Insights we had while exploring data that we didn’t anticipate:**
1.    We were surprised that trending videos overwhelmingly are ‘liked’ by users. With the exception of the ‘News and Politics’ category, in which ~15% of trending videos were disliked, all of the other categories had ‘likes’ > 97%. This seems to belie the old adage that ‘there is no bad publicity.’ It appears that ‘liked’ videos are the ones that trend, and that attempting to get views or publicity by attracting haters is a bad strategy.
2.    Music videos are the most likely to trend by far. This is unexpected, as a ‘video’’ is not needed to enjoy music, and as there are many competing music streaming services (Spotify, Apple). It turns out that ‘more music is played on youtube than on spotify, apple music and every other audio streaming platform combined.’ Youtube attracted 46% of all music streaming listening time, followed by 23% for paid audio platforms and 22% for free audio platforms. (Source: IFPI Global Music Report)
3.    It only takes, on average, 7 days for a video to trend, and if your video doesn’t trend within 10 days, it is unlikely to trend. This makes youtube very different from other media platforms, such as TV, where it takes between 1-3 seasons for a show to become a hit, or radio, where is typically takes 8-12 weeks for a song to reach the Top 40 after release.

Discuss any problems that arose after exploring the data, and how you resolved them.
1.    Youtube timestamps its videos in a non-standard format. We had to text parse the date format and convert the dates and times to the Python datetime format. We wrote a function to do this.
2.    Youtube uses integers instead of strings for its video categories. We had to download a category dictionary (which can change with time), and convert the category numbers to category names using the ‘replace’ function.
3.    Channel owners will often publish multiple copies of the same video using the same title, on different dates. These videos post as ‘unique’ videos with unique statistics. Ideally we would roll up statistics for duplicate videos into a single data point for our analysis. However, when we actually viewed videos with the same title from the same channel, we found that some videos would have subtle differences (for example, one video may have text pop-ups, and another not). We couldn’t figure out, short of watching ‘duplicate’ video with human eyes, if the videos were actually different and therefore shouldn’t be rolled up. So instead, we kept the ‘most popular’ instance of the duplicately-titled videos. Interestingly, the 2nd most popular instance of duplicately-titled videos typically had views that were orders of magnitude lower than the most popular video. So we feel our analysis still allows for significant inferences about the videos.

# Summary Statistics
## Top Five Liked Videos from August to November 2020
![top5videos](https://user-images.githubusercontent.com/70446836/98894950-ed89c480-2473-11eb-92b5-f54e4c0913e3.PNG)
The top five liked videos during this timeframe all fall in the music category; K-Pop groups seem to dominate this category.
## Most Published Videos per Category from August to November 2020
![mostpublishedcategories](https://user-images.githubusercontent.com/70446836/98894976-fc707700-2473-11eb-9c5f-0d67565e5ff0.png)
![mostpublishedcategoriesbar](https://user-images.githubusercontent.com/70446836/98895009-10b47400-2474-11eb-99ed-5c4aa2cff82c.PNG)
Music and entertainment publish the highest number of videos; surprisingly, Nonprofits and Activism had the least number of published videos with only five videos.
## Top Trending Channels from August to October 2020
![toptrendingchannelsbar](https://user-images.githubusercontent.com/70446836/98895742-66d5e700-2475-11eb-80f6-09c7cdb89226.PNG)
According to the top trending channel bar charts, the most popular channels in each month fall into either the music or entertainment categories. October is the exception as a gaming channel was the most popular as it reviewed the game Among Us.
## Relationship between View Count and Reactions per Category
![categoryscatter1](https://user-images.githubusercontent.com/70446836/98895232-a4864000-2474-11eb-98ed-fce942ac0cb6.png)
![categoryscatter2](https://user-images.githubusercontent.com/70446836/98895240-a6e89a00-2474-11eb-8ce3-2b282819e2bf.png)
These scatter plots display the relationship between view count and reactions per category. Reactions consist of the number of likes, number of dislikes, and number of comments.
## Comparison Between the Top Two Categories: Music vs. Entertainment:
![top2catscatter](https://user-images.githubusercontent.com/70446836/98895858-af8da000-2475-11eb-8ec2-ddb3cc258043.PNG)
Music and entertainment are the top two popular categories and have very similar reactions in regards to the number of likes and dislikes.
## Most relevant Videos in 2019
![Most watched videos in 2019df](https://user-images.githubusercontent.com/70446836/98896164-570ad280-2476-11eb-9e9a-b8edf93ffab8.png)
![Most watched videos in 2019 word cloud](https://user-images.githubusercontent.com/70446836/98896165-57a36900-2476-11eb-9b68-66815269db14.png)
## Most relevant Videos in 2020
![Most watched videos in 2020 df](https://user-images.githubusercontent.com/70446836/98896133-4b1f1080-2476-11eb-8338-072f345f6be5.png)
![Most watched videos in 2020 word cloud](https://user-images.githubusercontent.com/70446836/98896132-4b1f1080-2476-11eb-891d-ee6d1f5c3226.png)
The 2019 and 2020 word clouds contain key words from the most watched videos based on the comments. The most common words appear larger in the cloud.
## The Most Viewed Quarantine Challenge Videos During Strict COVID Lockdown
![quarantine challengebar](https://user-images.githubusercontent.com/70446836/98896182-60943a80-2476-11eb-82f4-c160173e882d.png)
![quarantine challenge word cloud](https://user-images.githubusercontent.com/70446836/98896184-60943a80-2476-11eb-97d8-26de7bac7d58.png)
The horizontal bar graph depict the most viewed quarantine challenge videos created during lockdown. This data was pulled from the YouTube Search API dataset and the word clouyd was generated from the comments.
# Findings and Observations
## Q1) Why were certain categories trending during specific times?
**Hypothesis**: Societal events will align with YouTube Trends (ex. quarantine challenges/vlogs, new music video releases, video games etc.)
**Actual Result**:
YouTube trends aligned with societal events accordingly based on the Top Five Liked Videos dataframe and the most popular categories bar chart. Music was the most popular category during this time and this was reflected as the top five videos were all related to K-Pop music groups, BTS and Blackpink.
According to the top trending channel bar charts, the most popular channels in each month fall into either the music or entertainment categories; these are the top two popular categories overall:
- August: Big Hit Labels was the most popular channel as BTS dropped music teasers and a video for their song, Dynamite.
- September: Blackpink was the most popular channel as Blackpink dropped a song with Selena Gomez called Ice Cream.
- October: The Pixel Kingdom, a gaming channel, was the most popular channel as it reviewed the hit game Among Us.
- November: JYB Entertainment is the most popular channel in November so far as another K-Pop Group, Twice, released new music.
## Q2) Is there a relationship between certain user behaviors: View Count, # of Likes, # Dislikes, # Comments
**Hypothesis**: If viewer count increases, viewer reactions will increase as well. This includes number of likes and dislikes as well as number of comments.
**Actual Result**: This hypothesis was proven false based on our analysis. According to our scatter plots, as view count increased, there was a decrease in reactions. The overall number of likes, dislikes, and comments gradually declined.
It was also observed that when videos are recently published and have a lower number of views, there is a stronger number of likes compared to dislikes and comments. This suggests that users interact with videos with likes rather than actively leaving comments as it is easier.
The scatter plots also displayed how the number of dislikes and comments remained consistant for the Entertainment and People & Blogs category.
If we focus solely on the top two categories, Music and Entertainment, we see that the scatter plots are very similar with the relationship between view count and reactions. Although, it does suggest that the music category as a stronger % of dislikes and likes when there is a lower view count compared to the entertainment category.
## Q3) Is there a difference in viewing habits from 2019 to 2020? Did the strict COVID lockdown in early 2020 impact viewer trends?
**Hypothesis**: Compared to 2019, YouTube viewing will increase in 2020. The lockdown will not affect the viewer trends because trends will remain consistant regardless social circumstances.
**Actual Result**: Based on the various data frames produced, the data suggests that YouTube viewing increased in 2020 compared to 2019. However, this maynot be an acurate mesurement as youtube videos published in 2019 can still be viewed today and will be counted towards their view value.  This may be due to the stay-at-home orders issued across the world due to the COVID pandemic.The top five videos pulled from the YouTube API datasets in 2019 and 2020 were all largely international videos:
In 2019, the top five videos:
1) Telegu News
2) TV5 News - Telegu News
3) Video Hub
4) Earth Views from Space
5) Turkish TV video

In 2020, the top videos:
1) Republic Bharat - Indian News
2) Haberturk TV - Turkish
3) Russian TV Show
4) Blackpink - Dance Practice
5) ABN Telegu News

During the strict COVID lockdown from March to June, there were no changes in viewer trends. Regardless of the pandemic, it seems that users continued to watch their typical videos, ranging from music to fitness, and entertainment. This is displayed from our YouTube API bar chart:
1) Diamond Platinumz - Quarantine (Tanzanian Artist)
2) Chloe Ting - Get Snatched During Quarantine
3) Quarantine Tik Tok Videos
4) Hello Neighbors Steals our Quarantine Games
5) SnowthaProducts- Nowhere to Go (Quarantine Love) (song created by a Mexican/American artist and rapper)

# Post - Mortem
**Difficulties**
- Due to the large datasets, with both the CSV and YouTube API, it was difficult to create a narrative for this project. The team had to figure out what data we wanted to pull and how we could connect the CSV and YouTube API datasets to form a bigger picture. We had a few meetings to discuss the overall importance and what the ultimate purpose was with our findings. All in all, it took time to figure out why we wanted this data and how it could prove useful for the YouTube community, whether that be investors or creators themselves.
- Another difficulty involved reading the API and performing the API calls itself. It was a challenge to repeatedly call the API without going over the quota. There are only so many requests we could do and we had to implement another method that allowed us to continue our analysis without overextending our API limit.
- Finding a commonality between the data frames in order to merge them effectively was another challenge. Some video IDs and channel IDs were actually dropped during the merge due to duplicates and irrelevancy.
- Lastly, it was difficult to set the appropriate axes' values for our charts. For a few charts, Billy and Desiree had to manually input the limits in order to maintain consistancy and display the correct values.
**Future Possibilities**
If we had two more weeks to work on this project, we would have conducted the following analysis:
- Revenue: At what point do channels earn the most money? Is it based off societal circumstances or the content itself that was published? How does one youtube creator earn more money compared on another popular creator? What are the factors that contribute to these earnings (view count, subscriber count, ad-sense, etc.)
- We are also interested in learning how to export large datasets from the csv in order to compare daily statistics between 2019 and 2020, but we are not sure how to export such large datasets.
- It would  be interested to predict subscriber count for trending channels. Is it possible forecast this number with the provided datasets?
- Comparsion between negative and positive comments. Which categories receive the largest negative reactions based on the comments. Is it possible to track the negative and positive comments in a effective way? Possibly use a word count for a comment section in the most popular/least popular videos in a given category.
