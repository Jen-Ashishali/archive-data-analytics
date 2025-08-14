# Project Objective
Wrangle and Store WeRateDogs Twitter data to create interesting and trustworthy analyses and visualizations.

# Wrangling
- The tweet archive was provided by Udacity and downloaded manually. Additional data queried from twitters API using
tweet ids present in the archive dataset, was downloaded manually and read line by line into a pandas dataframe. An
image prediction file from a neural network that classifies dog breeds contains a table of the top three image
predictions of dogs and was downloaded programmatically from Udacity’s servers with the Requests library.

- To assess each dataset for errors, visual and programmatic assessment was carried out. Details of data wrangling steps can be found in this [wrangle report](https://acrobat.adobe.com/link/review?uri=urn:aaid:scds:US:cda9ee1b-224c-34ff-8f49-e3131086f551) and in the wrangle_act notebook in this repository

# Analysis
This [act report](https://acrobat.adobe.com/link/review?uri=urn:aaid:scds:US:74d1cb29-f242-3535-9b8b-b77b0bfa7c09) contains details of the data analysis with supporting visualizations
# Date Created

22nd May 2022

# Project Title

Cyclistic Bike-share Project


# Table of Contents

1. Introduction

    - 1.1. Scenario

2. Business Task

    - 2.1. Statement of Business Task

3. Data Preparation

    - 3.1. Data Limitations
    - 3.2. Data Credibility

4. Data Processing

    - 4.1. Documentation of Cleaning

5. Data Analysis

    - 5.1. Key Findings and Differences

6. Data Vizualisation

7. Conclusion 

    - 7.1. Recommendation
    - 7.2. Credits
    
    
    
    

## 1. Introduction
This is a capstone project and is part of the prerequisites for completing the google data analytics professional course. In order to solve the business task, I will follow these steps of the data analysis process: **ask, prepare, process, analyze, share, and act**. 

### 1.1. Scenario
You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations

## 2. Business Task
This first step of the process, the **ask** phase will frame my business task and explain the problem I am trying to solve with these guiding questions;

- Who are the key stakeholders and what do they expect?

Director of Marketing, Cyclistic Executive Team, Cyclistic Marketing Analytics Team have a clear goal of designing marketing strategies aimed at converting casual riders into annual members.

- What is the problem?

How do annual members and casual riders use Cyclistic bikes differently?

### 2.1. Statement of Business Task

Analyze costumer segments to determine marketing strategies that maximize annual memberships.

## 3. Data Preparation

In this prepare phase, I will use Cyclistic’s historical trip data to analyze and identify trends. The trip data is public data made available by Motivate International Inc., under this [license](https://ride.divvybikes.com/data-license-agreement), and is stored as zip files organized by each year in 2013 – 2021. For the purpose of this analysis, 2021 dataset has been selected, stored in my hard drive, and organized by month in Excel files. N.B.: The datasets have a different name because Cyclistic is a fictional company.

### 3.1 Data Limitations
Data-privacy issues prohibit the use of riders’ personally identifiable information. This means that I cannot connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes. Large volume of missing data within start_lng, start_lat, end_lng, end_lat limits analysis of riders start location and destination. Also, demographic data for riders in 2021 dataset are unavailable.

### 3.2 Data Credibility
This third-party data is from a reliable source, and corresponds with the original source data on [Divvy data](https://ride.divvybikes.com/system-data). The dataset selected is current, comprehensive enough to solve the business task, and cited on [divvybikes.com](https://divvybikes.com/). We can conclude we are working with a good data source.

## 4. Data Processing

For the purpose of this analysis, Microsoft Excel for data cleaning, Python for further data wrangling and analysis, Tableau to visualize supporting data that informed recommendations, and Powerpoint for presentation of insights.

### 4.1. Documentation of Cleaning
Examine datasets for;
- Missing data
- Irrelevant data
- Duplicate entries
- Structural Errors
- Data Validation

- Missing data;
    - Create two columns in the spreadsheet **columns** and **missing_data**
    - Type each column name of the spreadsheet in **columns**. 
    - In the row next to each column name, under **missing_data** calculate for empty cells using the formula, =COUNTBLANK (column range). Where column range represents the cell address of all values within a column having matching name in **columns**.

  Columns **start_station_name, start_station_id, end_station_name, end_station_id** have > 5000 rows each with missing data for every month. To prevent this from skewing the result of the analysis, remove these columns with incomplete data.

- Irrelevant data;
    
     - **start_lat, start_lng, end_lng, end_lat** have been deleted as they work best with the columns found with missing data.
     - Delete **columns**, and **missing_data**

- Structural Errors
    - Add a filter to each column in the spreadsheet
    - Using the filter slice, check that each column has consistent entries, and there are no typos present in the observations.
    - Use the TRIM function to trim off whitespaces in ride_id column. Insert two columns next to ride_id, as column B and column C. In cell B2, enter =TRIM($A2), where A2 is the first observation of ride_id.
    - Copy the formula in B2. In the name box, type in the range of cells in column B you want the formula to be pasted. Once selected, click paste formula.
    - In column C, copy and paste the values in column B. Clear contents in ride_id, and replace with values in column C. Delete column B and column C.

- Duplicate Entries;

  The ride_id in column A is seen as unique identifier. To check that data isn’t repeated, check for duplicates within this column. 
    - Create a new column next to ride_id, named duplicates, as Column B
    - Use the formula =COUNTIF($A$2:$A$96835, $A2) in cell B2
    - The formula above returns the number of times the criteria “$A2”, appears in the range “$A2:$A$96835”. 
    - Copy the formula in B2 and paste in range B2:B96836.
    - The formula will adjust to reference the corresponding cell as new criterion
    - Add a filter to the column duplicates, and check for values > 1.
  No duplicates found within each month.

- Data Validation
    - Check that each column is formatted correctly with the appropriate data type
    - Check the length of characters for ride_id, rideabletype, and member_casual columns using the LEN function.
    - Insert a new column next to each column mentioned above
    - In the row of the new column (B) next to ride_id, input =LEN($A2) in cell B2. Where A2 is first value in ride_id. 
    - Copy the formula in cell B2. In the name box, enter the range of cells you want selected, and paste the copied formula. Repeat for rideabletype, and member_casual.
    - Sort the values of the new columns in ascending and descending order to identify the maximum and minimum values.
    - Apply data validation to ride_id, rideabletype, and member_casual using field length criteria as values between maximum and minimum values for ride_id, rideabletype and equal to text length of member_casual columns.

- Calculate and create columns with additional data for the purpose of this analysis.

  Ride Length
    - Create a column with name **duration**. Calculate the length of each ride by subtracting the column **started_at** from the column **ended_at** (for example, =D2-C2)
    - Format as HH:MM:SS using Format > Cells > Time > 37:30:55
    - Sort **duration** in ascending and descending order to examine outliers.
    - Delete rows with negative entries and values < 00:01:00
    - Create three columns **days, hour, minute, and seconds**
    - Extract the day, hour, minute and second from **duration** using =INT(D2-C2), =HOUR(MOD(D2-C2, 1)), =MINUTE(MOD(D2-C2, 1)), and =SECOND(MOD(D2-C2, 1)) respectively.
    - In a new column **ride_length**, combine **days, hour, minute, and seconds** (for example, =INT(D2-C2)&" days, "&HOUR(MOD(D2-C2, 1))&":"&MINUTE(MOD(D2-C2, 1))&":"&SECOND(MOD(D2-C2, 1)))

  Weekday
    - Create a column called **day_of_week**, and calculate the day of the week that each ride started using the “WEEKDAY” command (for example, =WEEKDAY(C2,1)) in each file. 
    - Format as General, noting that 1 = Sunday and 7 = Saturday.

## 5. Data Analysis

Descriptive Analysis will be carried out to explore different timelines which will yield insights,trends and comparisons within the two customer types. The datasets will be imported and aggregated in a jupyter notebook, [analysis.ipynb](https://github.com/Jen-Ashishali/Cyclistic-bikeshare-analysis/blob/main/analysis.ipynb) . 

### 5.1. Key findings/ Trends and Differences
   - Number of rides taken by Members are more than Casuals but Casual Riders take longer rides than Members. 
   - There is an increased number of Casual rides on weekends while Members have the more and consistent rides on weekdays
   - Casual rides were greater than members in June - August and were much lesser than Members in September – December
   - Number of rides for members increased at certain hours of the day from 6 am – 9 am and 5 pm – 7 pm
   - Members prefer Classic Bikes and Electric bikes while Casual use more docked bikes than members.
   - Longest ride for Casual is ~38days, which exceeds the expected frame for daily passes
   - May- September (Summer) is the busiest part of the month for both customers
   
## 6. Data Visualization 

A simple dashboard, [Bike-share Activity per Timeline](https://public.tableau.com/views/CyclististicBike-shareActivity/Activity?:language=en-GB&publish=yes&:display_count=n&:origin=viz_share_link), visually reveals trends within specific timelines about riders activity. A slide presentation, [Presentation](https://1drv.ms/p/s!ArqJe-n-XOU9hkmB965WXlarOXEC) summarizes the analysis, visualization and conclusion.

## 7. Conclusion
Cyclistic Members use ride share for routine daily activities like work, while Casual Riders use ride share for leisure activities. This conclusion is drawn on the key findings of;

   - Increased rides for Casual on weekends and greater consistent rides on weekdays for Members 
   - Rise in number of rides at common work schedule hours for members.
   - Increased activity for members and casuals during the summer months and reduced activity for mostly casual riders during the winter months.

### 7.1. Recommendation 

The **act** phase. Based on the characteristics of casual riders;

   - Improve membership plans by increasing flexibility in pricing plans that Casual Riders can leverage e.g., Monthly Membership plans, Weekend only Membership plans
   - Campaign should be done in periods with high ride activity for casuals e.g., Summer Months (May-September).
   - Ads should be placed in strategic areas e.g., leisure sites like parks, cyclistic docking stations

Evaluate impact of analysis in 6 months

### 7.2. Credits
I was able to complete this project by combining knowledge from Google Data Analytics Course, Python Documentation, and online search in google and stackoverflow.
