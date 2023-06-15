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
  4. Classic bikes are required to initiate and conclude their trips at docking stations, while electric bikes possess a lock and can be both started and finished anywhere       near a docking station.
  5. Trips with a duration of less than 1 minute or longer than 1 day are considered outliers and should be excluded from the analysis, as they typically represent               maintenance tasks performed by Cyclistic or instances where bikes have been stolen.

## Process

### Preliminary Analysis
Confirmed that each of the monthly datasets all have the same structure, number of columns, and data types.

<img width="200" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/d8f5064c-5a7d-4ff5-acf9-b1245698c648">

Combine the 12-months of bike-share data into one dataset.

<img width="400" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/b4e92f06-45ce-49bb-9202-ec1434d78d2d">

There are 5,595,063 rows of data.

![image](https://github.com/kdfields/Google_CapStone_Project/assets/113741694/cf0ada26-57a8-4630-8b77-0510bfe24484)

Every ride_id is unique so no removal of duplicates is necessary.

<img width="150" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/5cd182cf-7758-4da6-84c9-cd5a5a6de32c">

All the ride_ids are 16 characters in length.

<img width="250" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/6a57807a-57f5-46aa-a661-08a40b557156">

Confirmed three bike types: electric, classic, docked ('docked_bike' is named incorrectly and will be changed to 'classic' later).

<img width="150" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/324af70c-4040-4bf3-9567-5f9b7ffbc18d">

There are 163,630 trip durations of less than 1 minute or longer than 1 day that will be removed later.

<img width="150" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/f63ccd29-54c0-4ab2-b4da-6d6a7c044fa7">

Inspected start station names and found entries that need to be removed: '351' (bad name), 'Base-2132 W Hubbard Warehouse'(repair warehouse for bikes), and 'Lyft Driver Center Private Rack' (parking rack for Lyft )

<img width="250" alt="image" src="https://github.com/kdfields/Google_CapStone_Project/assets/113741694/93cde21d-d591-467d-8cd8-cd7d57abc98e">



