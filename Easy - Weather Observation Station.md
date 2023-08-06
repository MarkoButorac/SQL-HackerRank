**Weather Observation Station**

*NOTE:- Questions of Weather Observation Station from 1-17 -- # Difficulty: Easy*



**[Weather Observation Station 1](https://www.hackerrank.com/challenges/weather-observation-station-1)**

Query a list of CITY and STATE from STATION.

Input Format

The STATION table is described as follows:

|  Field | Type |
|---|---|
| ID  | NUMBER |
| CITY | VARCHAR2(21)   |
| STATE  | VARCHAR2(2)  |
| LAT_N |  NUMBER |
| LONG_W | NUMBER |

where LAT_N is the northern latitude and LONG_W is the western longitude.

**Solution**
```sql
SELECT CITY, STATE
FROM STATION;
```



**[Weather Observation Station 2](https://www.hackerrank.com/challenges/weather-observation-station-2)**

Query the following two values from the STATION table:

1. The sum of all values in LAT_N rounded to a scale of 2 decimal places.

2. The sum of all values in LONG_W rounded to a scale of 2 decimal places.

Input Format

The STATION table is described as follows:

|  Field | Type |
|---|---|
| ID  | NUMBER |
| CITY | VARCHAR2(21)   |
| STATE  | VARCHAR2(2)  |
| LAT_N |  NUMBER |
| LONG_W | NUMBER |

where LAT_N is the northern latitude and LONG_W is the western longitude.

*Output Format*

Your results must be in the form:

```lat lon```

where lat is the sum of all values in LAT_N and lon is the sum of all values in LONG_W. Both results must be rounded to a scale of 2 decimal places.



**Solution**
```sql
SELECT ROUND(SUM(LAT_N),2) AS ROUND_LAT_N,
       ROUND(SUM(LONG_W),2) AS ROUND_LONG_W
FROM STATION;
```



**[Weather Observation Station 3](https://www.hackerrank.com/challenges/weather-observation-station-3)**

Query a list of CITY names from STATION with even ID numbers only. You may print the results in any order, but must exclude duplicates from your answer.

Input Format

The STATION table is described as follows:

|  Field | Type |
|---|---|
| ID  | NUMBER |
| CITY | VARCHAR2(21)   |
| STATE  | VARCHAR2(2)  |
| LAT_N |  NUMBER |
| LONG_W | NUMBER |

where LAT_N is the northern latitude and LONG_W is the western longitude.

**Solution**
```sql
SELECT DISTINCT CITY
FROM STATION
WHERE MOD(ID,2) = 0
```



**[Weather Observation Station 4](https://www.hackerrank.com/challenges/weather-observation-station-4)**

Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.
The STATION table is described as follows:

Input Format

The STATION table is described as follows:

|  Field | Type |
|---|---|
| ID  | NUMBER |
| CITY | VARCHAR2(21)   |
| STATE  | VARCHAR2(2)  |
| LAT_N |  NUMBER |
| LONG_W | NUMBER |

where LAT_N is the northern latitude and LONG_W is the western longitude.

For example, if there are three records in the table with CITY values 'New York', 'New York', 'Bengalaru', there are 2 different city names: 'New York' and 'Bengalaru'. The query returns 1, because total number of records - number of unique city names.

**Solution**
```sql
SELECT COUNT(CITY) - COUNT(DISTINCT CITY)
FROM STATION;
```



**[Weather Observation Station 5](https://www.hackerrank.com/challenges/weather-observation-station-5)**

Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

Input Format

The STATION table is described as follows:

|  Field | Type |
|---|---|
| ID  | NUMBER |
| CITY | VARCHAR2(21)   |
| STATE  | VARCHAR2(2)  |
| LAT_N |  NUMBER |
| LONG_W | NUMBER |

where LAT_N is the northern latitude and LONG_W is the western longitude.

*Sample Input*

For example, CITY has four entries: DEF, ABC, PQRS and WXY.

*Sample Output*
```
ABC 3 

PQRS 4
```

*Explanation*
When ordered alphabetically, the CITY names are listed as ABC, DEF, PQRS, and WXY, with lengths  3,3,4 and 3. The longest name is PQRS, but there are  options for shortest named city. Choose ABC, because it comes first alphabetically.

*Note*
You can write two separate queries to get the desired output. It need not be a single query.


**Solution**
```sql
(SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) ASC, CITY
 LIMIT 1)
UNION
(SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY
LIMIT 1)
```



**[Weather Observation Station 6](https://www.hackerrank.com/challenges/weather-observation-station-6)**

Query the list of CITY names starting with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.

Input Format

The STATION table is described as follows:

|  Field | Type |
|---|---|
| ID  | NUMBER |
| CITY | VARCHAR2(21)   |
| STATE  | VARCHAR2(2)  |
| LAT_N |  NUMBER |
| LONG_W | NUMBER |

where LAT_N is the northern latitude and LONG_W is the western longitude.





