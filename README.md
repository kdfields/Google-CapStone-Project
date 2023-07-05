# Google_CapStone_Project
Final project for Google Data Analytics Professional Certification

## Introduction
This is the Google Capstone Project, the last step in completing the Google Data Analytics Professional Certfication.  The Google Data Analytics Professional Certfication emphasizes the six stages of the data analytics process **(Ask, Prepare, Process, Analyze, Share, Act)**.  Documentation on the Capstone Project can be found [here](https://www.coursera.org/learn/google-data-analytics-capstone).  This case study utilizes a bike-share company's data of its customers' trips over a 12-month period.  The data has been made available by this [data license agreement](https://ride.divvybikes.com/data-license-agreement).

## Scenario
I am a junior data analyst working on the marketing analysis team at Cyclistic, a bike-share company in Chicago.  The director or marketing believes the company's future sucess depends on maximizing the number of annual memberships.  Therefore, my team needs to better understand the bike-share business and how it operates.  From these insights, my team will will design a new marketing strategy to convert casual riders into annual members.  But first, Cyclistic executives must approve the recommendations, so they must be backed with compelling data insights and professional data visualizations.

## Ask
The director of marketing has been tasked with creating a marketing campaign with the goal of converting casual riders to annual members.  To better achieve this goal, the analytics team must answer the question, **How do casual riders and annual members use Cyclistic bikes differently?**

## Prepare
In order to address the given question, an examination of historical data from Cyclistic bike trips in the year 2022 will be conducted. The data, which is stored on Cyclistic's database, is reliable and unbiased, and has been organized into separate CSV files for each month. To facilitate the analysis, the 12 relevant CSV files have been saved locally.

To provide context, certain facts and limitations pertaining to the data have been outlined by Cyclistic's data collection team:

  1. Each month's data encompasses all bike trips that occurred during that specific period.
  2. To ensure privacy, any personally identifiable customer information has been removed from the data.
  3. The terms "docked bikes" and "classic bikes" refer to the same type of bicycles.
  4. Classic bikes are required to initiate and conclude their trips at docking stations, while electric bikes possess a lock and can be both started and finished anywhere near a docking station.
  5. Trips with a duration of less than 1 minute or longer than 1 day are considered outliers and should be excluded from the analysis, as they typically represent maintenance tasks performed by Cyclistic or instances where bikes have been stolen.

## Process

### Preliminary Analysis
Confirmed that each of the monthly datasets all have the same structure, number of columns, and data types.

<img width="200" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/d8f5064c-5a7d-4ff5-acf9-b1245698c648">

Combine the 12-months of bike-share data into one dataset.

<img width="400" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/b4e92f06-45ce-49bb-9202-ec1434d78d2d">

There are 5,595,063 rows of data.

![image](https://github.com/kdfields/Google_CapStone_Project/assets/113741694/cf0ada26-57a8-4630-8b77-0510bfe24484)

### I inspected each column in the data set, notating what columns need to be cleaned prior to the exploratory analysis phase.

* Every ride_id is unique so no removal of duplicates is necessary.

<img width="150" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/5cd182cf-7758-4da6-84c9-cd5a5a6de32c">

* All the ride_ids are 16 characters in length.

<img width="250" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/6a57807a-57f5-46aa-a661-08a40b557156">

* Confirmed three bike types: electric, classic, docked ('docked_bike' is named incorrectly and will be changed to 'classic' later).
<img width="124" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/5e6237a4-be0a-4bb1-b5fd-4a65d49ff031">


* There are 163,630 trip durations of less than 1 minute or longer than 1 day that will be removed later.

<img width="90" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/f63ccd29-54c0-4ab2-b4da-6d6a7c044fa7">


* Inspected start and end station names and found entries that need to be removed: 'Null' (no station name),'351' (bad name), 'Base-2132 W Hubbard Warehouse'(repair warehouse for bikes), 'Divvy Cassette Repair Mobile Station' (mobile repair station), and 'Lyft Driver Center Private Rack' (parking rack for Lyft riders).  Some of the valid station names have leading or trailing spaces that will need to be cleaned.

<img width="250" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/93cde21d-d591-467d-8cd8-cd7d57abc98e">

<img width="250" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/413827cc-ee16-4fc9-8260-721d26d88e6b">

* Classic and docked bikes are required to start and end their trips at a docking station, but electric bikes may be locked up 
nearby using attached bike locks; these trips do not require a start and end station name.  Classic/docked bikes with no  
start and end station name will be removed and electric bikes with no start and end station names will be changed to 'On Bike Lock'.

<img width="250" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/5d94c257-9712-4783-a848-6099b1861fed">

* Approximately 4771 rows are missing data on the starting or ending latitude and longitude.  These rows will be removed as these locations cannot be mapped.

  <img width="120" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/a8de049a-4068-4801-be13-d85479a4cdb8">

* Confirmed that there are two types of riders: casual and members.  Casual riders pay by the trip and members pay a monthly subscription fee.
  
  <img width="122" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/432d00eb-a774-4892-8067-9a987f6c51a3">

### Data Cleaning
After conducting the preliminary analysis, I have identified the next steps in the data cleaning process.  Some of the data needs to be cleaned further, or removed completely, and some new columns need to be created using the data available to further assist our analysis. Here is one example of the queries used to clean the data further.

<img width="450" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/28432b32-52c4-4335-9a08-36cf8e9c5445">


A summary of the data cleaning steps taken can be described as follows:

1. Trips involving classic bikes were removed if either the start or end station had null values.
2. Trips with missing latitude or longitude values for the start or end locations were removed.
3. The label 'docked bike' was replaced with 'classic bike'.
4. Leading and trailing spaces in the start and end station names were removed to ensure consistency.
5. Null values in the start and end station name columns were replaced with 'On Bike Lock' for electric bikes only.
6. Additional columns were created to include the day of the week, month, year, and ride time length for analysis purposes.
7. Trips with extremely short (less than/equal to 1 minute) or long (greater than/equal to 1 day) ride times were removed.
8. Trips associated with bike maintenance stations were excluded.
9. As a result of these cleaning steps, a combined table with 5,424,330 rows remained after removing 170,733 rows.

## Analyze/Share
To understand the question, **How annual members and casual riders utilize Cyclistic bikes differently?**, the data was thoroughly cleaned and then analyzed. The analysis process involved using SQL queries to sort, filter, and aggregate the data prior to exporting the data to Tableau for data visualizations.  Here is an example of one of the queries used:

<img width="480" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/a574ccd5-c96d-4c17-8ffa-e28c2bbc3fac">

### Discoveries
<img width="779" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/7232196f-1c7d-4017-b406-ff872232365f">

In 2021, the majority of trips taken were by annual members, making up 54.5% of the total, while casual riders accounted for 45.5% of the rides. Both groups showed a preference for classic bikes over electric bikes. However, casual riders used electric bikes at a slightly higher proportion compared to classic bikes, with 37.3% of their rides being electric bikes, compared to 34.9% for annual members. It is worth noting that this difference is not considered statistically significant.

I analyzed the overall bike trip data for 2021, considering the number of trips based on the month and time of day.

<img width="593" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/45d31df3-9c4b-4343-9140-638000c6bf70">


Based on the line graphs, it is clear that casual members show a preference for riding bikes during late spring through the end of summer, while their ridership declines in the winter months, possibly due to unfavorable weather conditions. On the other hand, annual members also prefer riding bikes during the spring and summer but exhibit more consistent ridership levels throughout the year. Notably, the ridership of annual members significantly increases between 6am and 8am, peaking between 4pm and 6pm, and drops significantly after 7pm. In contrast, casual ridership remains relatively stable throughout the day without any sharp spikes.

Based on these observations, we can hypothesize that annual members primarily use Cyclistic bikes for commuting, as their ridership peaks during typical work commute hours and declines outside of those hours. Additionally, annual members display less of a decline in ridership during the winter months compared to casual members. Hence, it is plausible to speculate that casual members utilize Cyclistic bikes more for recreational or leisure purposes.

To further investigate this hypothesis, I proceeded to analyze the ridership levels based on the day of the week and average ride duration measured in minutes.

<img width="552" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/af8596c8-4246-40ea-b92c-dfdc96da7239">

Based on the line graphs, it is evident that annual members maintain a consistent level of ridership throughout the workweek, with a slight decrease on weekends. In contrast, casual ridership is lower during weekdays but experiences a significant increase during the weekend. Moreover, the average ride duration for annual members is 13.23 minutes, while casual riders have an average ride duration of 25.98 minutes, nearly twice as long.

These findings strongly support our hypothesis that annual members primarily use Cyclistic bikes for weekday commuting, taking short trips to and from work. On the other hand, casual riders tend to use Cyclistic bikes on the weekends for recreational purposes, enjoying longer rides.

To gain further insights, we now turn our attention to a map of Chicago that displays the starting locations of bike trips. The map categorizes the bike trips by member type and excludes electric bike trips where a bike lock was used. Additionally, the map is filtered to show only the top 10 locations with the highest frequencies of starting trips for each member type.

<img width="817" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/11579022-4941-4796-b0c9-5adc9f7e6aef">

It is evident that the most popular starting stations for casual members are typically located near bodies of water and large parks. On the other hand, annual members tend to commence their bike trips more centrally, closer to Chicago's financial district, office complexes, and residential buildings.

Let's shift our focus to examining the top 10 destinations where bike rides conclude, specifically excluding trips where a bike lock was utilized.

<img width="792" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/47c2c929-894b-4856-9a2a-ea78f9a79fd1">

The maps reflect a consistent pattern where casual riders tend to prefer areas in proximity to parks, waterfronts, and piers, while annual members are more inclined to frequent commercial zones. Interestingly, the top 5 stations visited by casual riders are the same for both their starting and ending points. These stations, namely Streeter Dr & Grand Ave (the pier), Millennium Park, Theater on the Lake, and Shedd Aquarium, are prominent tourist attractions and recreational spots. In contrast, none of these stations rank within the top 5 for annual members, suggesting that recreational activities and sightseeing hold lesser importance for this group.

**Summary of Insights:**
Casual Riders:
+ Primarily use Cyclistic bikes for leisure, preferring midday rides on weekends, particularly during late spring and early summer.
+ Their average ride duration is approximately twice as long as that of annual members.
+ Tend to start and end their trips near water bodies, city parks, and tourist/recreational attractions.
Annual Members:
+ Predominantly use Cyclistic bikes for commuting, with year-round weekday rides, especially during peak work commuting hours. Winter months show a slight decrease in ridership.
+ The average ride duration for annual members is approximately half that of casual riders.
+ Typically start and end their trips in urban areas near office and apartment buildings.

## Recommended Actions:

After analyzing the disparities between casual riders and annual members, the marketing department can now focus on converting casual riders into long-term annual members. However, it's important to note that a significant portion of casual riders are likely tourists who may not be interested in becoming annual members. Nonetheless, I have formulated the following recommendations aimed at converting Chicago residents who are casual riders into loyal annual members:

+ Introduce new subscription plans: Cyclistic can offer specialized plans such as the 'Warm-Weather Member' or 'Weekend Member.' The 'Warm-Weather Member' plan would provide discounted unlimited bike usage during the six months of spring and summer. Similarly, the 'Weekend Member' plan would offer unlimited bike access every Friday, Saturday, and Sunday throughout the year.

+ Optimize advertising campaigns: To maximize impact, advertising campaigns should be launched during the summer months when casual ridership is at its peak. This ensures the message reaches the largest audience possible. Additionally, setting up informational and promotional booths on weekends near popular starting and ending stations for casual riders, such as the Chicago Pier and Millennium Park, can help engage potential members and provide them with relevant details.

By implementing these strategies, Cyclistic can refine its marketing approach to target Chicago residents who currently use the service casually, aiming to convert them into long-term annual members.







