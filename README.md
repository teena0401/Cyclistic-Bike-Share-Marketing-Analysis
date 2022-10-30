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
-- retrieving filtered and cleaned data --- 
CREATE VIEW cyclistic.TRIPDATA AS SELECT
distinct(ride_id),
rideable_type,
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

<img src="https://i.imgur.com/JOUZW7q.png" height="300" width="450">

#### User
Looking at the total count of trips for each day of the week, members take more trips during the weekdays than casual riders; except during weekends, the number of trips taken by casual riders exceed members. We then can decude that majority of the member users using bikes for commuting to workplace. This can be further supported by looking at the numbers of riders taken throughout a day

<img src="https://i.imgur.com/X8WaZkv.png" height="300" width="450">


#### Hourly Traffic Analysis of Users

Here, we can see that members take more bike rides overall than casual riders throughout the day. Ridership peaks around 8am, 12pm, and 6pm, suggesting an increase in rides during the morning, lunch, and evening rush hours of the day.
 <img src="https://i.imgur.com/ghp4lWs.png" height="300" width="450">

#### Monthly User Traffic 
Looking at the combined year, casual riders exceed members in number of bike rides between mid-May and mid-August, perhaps suggesting an increase in locals on vacation and tourists visiting Chicago during the summer months.
<img src="https://i.imgur.com/rBuNeX0.png" height="300" width="450">

#### Most Popular Stations for Casual Users 
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
- Their average trip duration is 6 minutes longer than members riders 
- Their ridership peaks above members during the summer months



##### Recommendations 

Implement advertising annual memberships prices more using billboards/posters near the top 20 most popular stations for casual users.
Provide a limited discount on annual memberships purchased during the months of lowest traffic to increase rider usage in these months.
Have frequent advertisements on social media and television during peak hours and peak months, since that is when most people have a thought about riding bikes.
Consider provide free ride minutes for every minute passed after 30 minutes of usage, where the free minutes can ONLY be redeemed on weekdays to help promote rider usage during weekdays.
Now that I have defined the key differences between members and casual riders, the marketing department is able to come up with some strategies that can help market the annual membership to casual riders and convert them into members.

I recommend launching a marketing campaign highlighting the benefits of having an annual membership pass. Rather than paying for each trip, Cylistic should emphasize to casual riders the lower-cost per hour compared to not having an annual membership. We should offer exclusive benefits for members such as a priority access pass that enables them to secure a bike up to an hour in advance by making reservations through the app.

Cyclistic could also create a weekend membership pass providing casual riders with unlimited rides on the weekend. This could help persuade casual riders into purchasing an annual membership.

Lastly, we could launch tiered weekly and monthly passes to capture casual riders in the market who cannot commit to an annual pass. This could be especially appealing during the summer months when the ridership of casual riders exceeds that of annual members.

