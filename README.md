# Bikes_Google_Capstone
Capstone Project for the Google Data Analytics' Certification Programs

--After cleaning some of the data in Excel by deleting column I will not be using. I loaded all 12 months data into SQL and unioned them all together to create one table

SELECT*
FROM SQLTutorial.dbo.April2022
UNION
SELECT*
FROM SQLTutorial.dbo.May2022
UNION
SELECT*
FROM SQLTutorial.dbo.March2022
UNION
SELECT*
FROM SQLTutorial.dbo.Feb2022
UNION
SELECT*
FROM SQLTutorial.dbo.Jan2022
UNION
SELECT*
FROM SQLTutorial.dbo.Dec2021
UNION
SELECT*
FROM SQLTutorial.dbo.Nov2021
UNION
SELECT*
FROM SQLTutorial.dbo.Oct2021
UNION
SELECT*
FROM SQLTutorial.dbo.Sept2021
UNION
SELECT*
FROM SQLTutorial.dbo.Aug2021
UNION
SELECT*
FROM SQLTutorial.dbo.July2021
UNION
SELECT*
FROM SQLTutorial.dbo.Jun2021



Select*
FROM SQLTutorial.dbo.April2022

--Making sure the dataset looks clean and loading properly. Also ordering ridelength by longest ride to shortest.

Select*
FROM SQLTutorial.dbo.bike_capstone_cleaned
ORDER BY ridelength desc

--Calculating total of type of bikes casual and members like to ride ranking highest to lowest

SELECT memberorcasual, ridetype, count(ridetype) total
FROM SQLTutorial.dbo.bike_capstone_cleaned
GROUP By memberorcasual, ridetype
ORDER BY 1,3 desc

--Calculating most popular days of week for casual and member riders

SELECT memberorcasual, dayoftheweek, count(dayoftheweek) totaldayofweek
FROM SQLTutorial.dbo.bike_capstone_cleaned
GROUP By memberorcasual, dayoftheweek
ORDER BY memberorcasual, totaldayofweek desc

--Using CTE to partition members from casual riders to see total casual riders compared to members that rode over 20 minutes

WITH over_20_ride AS
(
SELECT memberorcasual, ridelength, COUNT(ridelength) as total_ridelength
FROM SQLTutorial.dbo.bike_capstone_cleaned
WHERE ridelength > '20:00:00'
GROUP By memberorcasual, ridelength
)

SELECT ridelength, memberorcasual, COUNT(ridelength) OVER (PARTITION BY memberorcasual) AS ridertype
FROM over_20_ride
ORDER BY memberorcasual, ridelength desc





