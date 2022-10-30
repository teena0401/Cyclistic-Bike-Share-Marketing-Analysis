### Introduction 
Cyclistic is a Bike-Sharing coompany based in Chicago that possess more than 5,800 bicycles and 600 docking stations. Cyclistic users are more likely to use their bikes for leisure, but about 30% use them to commute for work each day. Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. The company offers single day passes, full day passes for a price for casual users, and provie an annual subscription fee for its members. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

Cyclistic has concluded that annual members are much more profitable than casual riders. Therefore, maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, they believe creating a marketing campaign solely focused on casual users would help convert casual users into members. The company has set a clear goal of designing marketing strategies aimed at converting casual users into members. In order to do so they need to better understand the difference between how casual users differ from subscribed members and interest in analyzing the historical bike data trip to help identify trends.


### Problem Statements 
The Company's analysts have inferred that annual members are much more profitable for the company than casual users, so they believe that the key of the company's future is depended upon maximizing the number of annual memberships.

The business-related problem statements that could be asked to improve the company's growth rate and success is shared below:

1. How do casual users and annual subcribed members use Cyclistic Bikes differently?
2. How can we design new marketing strategies to help convert casual members into annual members?

### Preparing Data for Analysis
 
For this project, I've used the 13 trip-data datasets dated from April 2020 to April 2021. Click on this link to access the website and download the datasets provided as .zip files. The data provided in this website is made available to access to the public.

Or you could access and download the data from this repository named as "Raw Data".

I am using Microsoft SQL Server Management Studio in this part of the project to help process and analyze the datasets.

First make sure to import all of the dataset as a .csv file to the database server. Check and verify if the data types of each of the columns in each dataset is same to merge them all together.

NOTE: the start_station_id column of dataset from Dec 2020 to April 2020 contains string values

```sql
CREATE TABLE tripdata_2021A (ride_id VARCHAR(225) ,rideable_type TEXT, started_at VARCHAR(225),ended_at VARCHAR(225),start_station_name VARCHAR(225),start_station_id VARCHAR(225),end_station_name VARCHAR(225),
end_station_id TEXT,start_lat VARCHAR(225),start_lng VARCHAR(225),end_lat VARCHAR(225), end_lng VARCHAR(225),member_casual TEXT ,ride_length VARCHAR(225),day_of_week INT);
```

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

### Processing and Analysis of Data 

 ```sql
-- filerting and cleaning the datatype --- 
CREATE VIEW cyclistic.TRIPDATA AS SELECT
ride_id  ,
rideable_type ,
cast(str_to_date(started_at,'%d/%m/%y %H:%i') as datetime) as started_at,
cast(str_to_date(ended_at,'%d/%m/%y %H:%i') as datetime) as ended_at,
start_station_name, 
start_station_id ,
end_station_name ,
end_station_id ,
start_lat ,
start_lng ,
end_lat,
end_lng,
ride_length,
member_casual ,
day_of_week,
 (CASE 
when day_of_Week = 1 then 'Sunday' 
when day_of_Week = 2 then 'Monday' 
when day_of_Week = 3 then 'Tuesday'
when day_of_Week = 4 then 'Wednesday'
when day_of_Week = 5 then 'Thursday'
when day_of_Week = 6 then 'Friday'
when day_of_Week = 7 then 'Saturday'
end ) AS weekday_weekend,
cast(concat(cast(start_lng as char) , cast(start_lat as char)) - CONCAT(cast(end_lng as char) ,cast(end_lat as char)) as float) as ride_distance,
MINUTE(timediff(ended_at , started_at)) as ride_length_2
FROM cyclistic.tripdata_2021
WHERE start_station_name !='' and  end_station_name != '' 
HAVING ride_length_2 > MINUTE(0)
```
[summary statistics] 

## Data Visualization 

#### Average Ride Duration: 
#### User
#### Hourly Traffic Analysis of Users
#### Monthly User Traffic 
#### Most Popular Stations for Casual Users 


## Conclusion 

