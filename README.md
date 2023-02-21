### Introduction   
Cyclistic is a Bike-Sharing coompany based in Chicago that possess more than 5,800 bicycles and 600 docking stations. Cyclistic users are more likely to use their bikes for leisure, but about 30% use them to commute for work each day. Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. The company offers single day passes, full day passes for a price for casual users, and provie an annual subscription fee for its members. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

### About Cyclistics   
Cyclistic has concluded that annual members are much more profitable than casual riders. Therefore, maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, they believe creating a marketing campaign solely focused on casual users would help convert casual users into members. The company has set a clear goal of designing marketing strategies aimed at converting casual users into members. In order to do so they need to better understand the difference between how casual users differ from subscribed members and interest in analyzing the historical bike data trip to help identify trends.

### Method Approach    
# Phase 1. Ask 

### 1.1: Business Task   
The Company's analysts have inferred that annual members are much more profitable for the company than casual users, so they believe that the key of the company's future is depended upon maximizing the number of annual memberships. The business-related problem statements that could be asked to improve the company's growth rate and success is shared below:

1. How do casual users and annual subcribed members use Cyclistic Bikes differently?
2. How can we design new marketing strategies to help convert casual members into annual members?

### 1.2: Key Stakeholders    

# Phase 2. Prepare
### 2.1: Dataset Used 

In this project, I used datasets which provided by this google course and has been made available by Motivate International Inc. This public data that you can explore how different customer types are using Cyclistic bikes. 

### 2.2: Dataset Summary 
I downloaded zip files provided, then extracted to csv files. There are 12 datasets.Each file represents different month of rider data. 

The following summary has listed tables that I selected for this project.
<img src = "https://imgur.com/OHa9nRL.png">

### 2.3: Dataset Limitations and Integrity

# Phase 3. Process 
### 3.1: Importing Datasets 

For this project, I've used the 13 trip-data datasets in 2021 year. Click on this link to access the website and download the datasets provided as .zip files. The data provided in this website is made available to access to the public.
Or you could access and download the data from this repository named as "Raw Data".

I am using MySQL in this part of the project to help process and analyze the datasets. First make sure to import all of the dataset as a .csv file to the database server. Check and verify if the data types of each of the columns in each dataset is same to merge them all together.

NOTE: the start_station_id column of dataset from Dec 2020 to April 2020 contains string values

```sql

- Due to large data file, I created table for each month and imported file by month before merging them into one. 

--- January---
CREATE TABLE tripdata_202101 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202101-divvy-tripdata.csv'
INTO TABLE tripdata_202101
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---February---
CREATE TABLE tripdata_202102 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202102
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---March---
CREATE TABLE tripdata_202103 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202103-divvy-tripdata.csv'
INTO TABLE tripdata_202103
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---April---
CREATE TABLE tripdata_202104 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202104-divvy-tripdata.csv'
INTO TABLE tripdata_202104
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---May---
CREATE TABLE tripdata_202105 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202105
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---June---
CREATE TABLE tripdata_202106 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202106
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---July---
CREATE TABLE tripdata_202107 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202107
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---August---
CREATE TABLE tripdata_202108 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);

LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202108
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---September---
CREATE TABLE tripdata_202109 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202109
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---October---
CREATE TABLE tripdata_202110 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202110
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---November---
CREATE TABLE tripdata_202111 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202111
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 

---December---
CREATE TABLE tripdata_202112 (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
LOAD DATA INFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\Cyclistic.XLS\\202102-divvy-tripdata.csv'
INTO TABLE tripdata_202112
FIELDS TERMINATED BY ','
ENCLOSED BY ""
LINES TERMINATED BY '\n'
IGNORE 1 ROWS; 
```

### 3.2: Merging Datasets

After importing the data into mysql database, merging them into one table (cyclistic.tripdata_2021)

```sql
CREATE TABLE tripdata_2021 AS(SELECT ride_id ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week 
FROM cyclistic.tripdata_202101
UNION ALL 
SELECT ride_id, rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202102
UNION ALL 
SELECTride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202103
UNION ALL 
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202104
UNION ALL
SELECTride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202105
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202106
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202107
UNION ALL
SELECTride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202108
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202109
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202110
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202110
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week 
FROM cyclistic.tripdata_202111
UNION ALL
SELECT ride_id  ,rideable_type ,started_at ,ended_at ,start_station_name ,start_station_id ,end_station_name ,end_station_id ,start_lat ,start_lng ,end_lat ,end_lng ,member_casual ,ride_length ,day_of_week FROM cyclistic.tripdata_202112);
```
### 3.3 Cleaning Data 
This section is filtering, transforming and 

In the previous section, the datatype of started_at and ended_at columns suppose to be datetime. However, I input it as string datatype. 
Hence, both columns are needed to be casted as datetime. 

 ```sql
-- retrieving filtered and cleaned data --- 

CREATE VIEW cyclistic.TRIPDATA AS SELECT
distinct(ride_id), ---------------------------------------------------------- remove the duplicate value 
rideable_type,
cast(str_to_date(started_at,'%d/%m/%y %H:%i') as datetime) as started_at, --- cast the field to datetime type while retrieving other columns 
cast(str_to_date(ended_at,'%d/%m/%y %H:%i') as datetime) as ended_at,     --- cast the field to datetime type while retrieving other columns 
start_station_name, 
start_station_id ,
end_station_name ,
end_station_id ,
start_lat ,
start_lng ,
end_lat,
end_lng,
member_casual ,
WEEKDAY(started_at) AS day_of_week, ------------------------------------------ use WEEKDAY function to sort out the day of week for each recor222222`d
 (CASE 
when day_of_Week = 6 then 'Sunday' 
when day_of_Week = 0 then 'Monday' 
when day_of_Week = 1 then 'Tuesday'
when day_of_Week = 2 then 'Wednesday'
when day_of_Week = 3 then 'Thursday'
when day_of_Week = 4 then 'Friday'
when day_of_Week = 5 then 'Saturday'
end ) AS weekday_weekend,
MINUTE(datediff(ended_at , started_at)) as ride_length ----------------------- using the DATEDIFF function to calculate the ride length of each users
FROM cyclistic.tripdata_2021
WHERE start_station_name !='' and  end_station_name != '' 
HAVING ride_length > MINUTE(0)
```

# 4. Analyze (Tableau)
# 5. Share (Findings)
# 6. Act  (Recommendations)

### Preparing Data for Analysis


## Data Visualization 
In this section, I have chosen tableau to visualize my cleaned datatset. 

#### Average Ride Duration:    
<img src="https://i.imgur.com/JOUZW7q.png" height="300" width="450">

#### Trip count per rider 
Looking at the total count of trips for each day of the week, members take more trips during the weekdays than casual riders; except during weekends, the number of trips taken by casual riders exceed members. We then can decude that majority of the member users using bikes for commuting to workplace. This can be further supported by looking at the numbers of riders taken throughout a day  
<img src="https://i.imgur.com/X8WaZkv.png" height="300" width="450">


#### Hourly Traffic Analysis of Users
Here, we can see that members take more bike rides overall than casual riders throughout the day. Ridership peaks around 8am, 12pm, and 6pm, suggesting an increase in rides during the morning, lunch, and evening rush hours of the day.    
 <img src="https://i.imgur.com/ghp4lWs.png" height="300" width="450">

#### Monthly User Traffic 
Looking at the combined year, casual riders exceed members in number of bike rides between mid-May and mid-August, perhaps suggesting an increase in locals on vacation and tourists visiting Chicago during the summer months.     
<img src="https://i.imgur.com/rBuNeX0.png" height="300" width="450">

#### Most Popular Stations for Riders  
Top 10 popular station for casual and member users    
<img src="https://i.imgur.com/KibFps2.png" height="300" width="450">

## Conclusion 
 
#### Findings
Members: 
- Members are most likely daily traveller who take bikes consistently during weekday than casual riders. 
- Their average trip duration of 12.83 minutes is seven minutes lesser than the average trip length of casual users. 
- Their ridership peaks around rush hour time during the day but decline during winter months

Casual Riders: 
- Casual Riders may be a mixture of locals and tourists who ride bikes for longer period of time and more often on the weekend. 
- Their average trip duration is twice longer than average ride length of members riders 
- Their ridership peaks above members during the summer months



##### Recommendations 
I recommend a marketing campaign pinpointing the perks of subscribing to membership pass such as lower cost per hour, access to advance booking system, and loyalty program. 
- The place near the top 20 most popular stations should advertise heavily because it has the highest traffic across 200 stations which contributing to huge part of the profit. 
- During the cold season such as winters, promotion on membership could be considered to increase the ridership during the off season. 
- The social media marketing or advertisement should be more frequent during the peaks of days ( 8am, 12pm, 6pm) , months (summers). 
