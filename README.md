# SQL--UK_Accidents_2016_Casestudy

![michael-jin-ipHlSSaC3vk-unsplash](https://user-images.githubusercontent.com/116425101/201458301-8767b79b-12c1-44c4-b753-fe65625024fe.jpg)

This project is about UK accidents reported in 2016. I have used SQL(MySQL) for Analysis.


There is public dataset available for UK accidents from year 1979 to 2020.
I have cleaned it and used only 2016 data. The dataset of 2016 have 1,36,621 records. There are multiple variable(total 12 attributes) in dataset like Districts, Highway Authority, Raod condition, Light condition, Weather condition, Area type etc.

I have created tables for each variable. During the query, I have joined them with main table as and when required.

Let's start the analysis.

### (1) Number of accidents reported in 2016
SELECT count(*) as total_accidents  
FROM accidents_2016  

![image](https://user-images.githubusercontent.com/116425101/201454235-946eb521-6bd0-4412-8d0e-6d96025387c6.png)


### (2) Month Wise accidents in ascending order
SELECT month_name, count(*) as total_accidents  
FROM accidents_2016  
GROUP BY month_name  
ORDER BY total_accidents desc 

![image](https://user-images.githubusercontent.com/116425101/201454421-24902fa3-be18-48f8-8d3b-f0d489084a5d.png)

We can see February, March and April have the lesser number of accidents reported. Cold weather during this time can be one of the reason but we can not be so sure as the difference in accident numbers between these three months and other months is not big. 

### (3) Top 10 District with highest accidents
SELECT dn.district, count(*) as total_accidents  
FROM accidents_2016 ac  
JOIN district_name dn ON ac.local_authority_district = dn.id  
GROUP BY dn.district  
ORDER BY total_accidents desc  
LIMIT 10  

![image](https://user-images.githubusercontent.com/116425101/201456160-23aee838-2c11-4fcf-9185-a4ee855fb270.png)

Birmingham have the highest number of accidents reported.  

### (4) Reasons for the accidents  
We have carriageway_hazard table with the possible reasons of accidents.  

SELECT ch.hazard_type, count(*) as total_accidents  
FROM accidents_2016 ac  
JOIN carriageway_hazard ch ON ac.carriageway_hazards = ch.id  
GROUP BY ch.hazard_type  
ORDER BY total_accidents desc  

![image](https://user-images.githubusercontent.com/116425101/201456444-90bd8f2b-5712-4537-97a5-a783e62e59ba.png)
  
98% of reported accidents have reason mentioned as None. So this data is not giving any information about possible reasons and hence it is not so useful for our analysis.  

### (5) Top 10 Highway Authorities where maximum accidents reported  
SELECT ha.highway_auth, count(*) as total_accidents  
FROM accidents_2016 ac  
JOIN highway_authority ha ON ac.local_authority_highway = ha.id  
GROUP BY ha.highway_auth  
ORDER BY total_accidents desc  
LIMIT 10  

![image](https://user-images.githubusercontent.com/116425101/201456740-d03b78dc-46cc-4df9-abd4-4f186355896d.png)
  

Kent and Surray highway authority have reported maximum number of accidents.  

### (6) Road condition wise accidents in Highest accident district 'Birmingham'  
SELECT rc.road_condition, count(*) as total_accidents  
FROM accidents_2016 ac  
JOIN	district_name dn ON ac.local_authority_district = dn.id  
JOIN	road_condition rc ON ac.road_surface_conditions = rc.id  
WHERE dn.district = 'Birmingham'  
GROUP BY rc.road_condition  
ORDER BY total_accidents desc  

![image](https://user-images.githubusercontent.com/116425101/201457224-1aae6a74-0e68-4614-8eab-798ec2b42f1e.png)

Looks like most of the accidents in Birmingham happened on the noral day. Road condition is not a big factor in this case.  

### (7) Role of Light conditions in accidents  
SELECT lc.light_condition, count(*) as total_accidents  
FROM accidents_2016 ac  
JOIN light_conditions lc ON ac.light_conditions = lc.id  
GROUP BY lc.light_condition  
ORDER BY total_accidents desc  

![image](https://user-images.githubusercontent.com/116425101/201457897-a4d54abe-4b3e-4a21-bea0-a33b29281496.png)
  
Around 72% accidents happened in Daylight and remaining in Darkness.  

### (8) Urban Vs Rural Accidents  
SELECT area_type, count(*) as total_accidents  
FROM accidents_2016  
GROUP BY area_type  

![image](https://user-images.githubusercontent.com/116425101/201458058-f29b8bb5-eb69-494c-b1cd-414814beeb6d.png)
  
65-35 is the ratio of accidents in Urban Vs Rural.


## I hope you liked the analysis. Please share your feedback.

# Thanks!





