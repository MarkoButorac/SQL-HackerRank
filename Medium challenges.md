                                                        Advance Select
                                                    

**[The PADS](https://www.hackerrank.com/challenges/the-pads)**

Generate the following two result sets:

1. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).

2. Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format: 

        There are a total of [occupation_count] [occupation]s.

where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

Note: There will be at least two entries in the table for each type of occupation.

**Input Format**

|  Column | Type |
|---|---|
| Name  | String |
| Occupation  | String |

The OCCUPATIONS table is described as follows: Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

**Sample Input**

An OCCUPATIONS table that contains the following records:

|  Name | Occupation |
|---|---|
| Samantha  | Doctor |
| Julia | Actor |
| Maria | Actor  |
| Meera | Singer |
|Ashely | Professor |
|Ketty| Professor | 
|Christeen | Professor |
|Jane| Actor)|
|Jenny| Doctor |
|Priya| Singer |

  **Sample Output**
  ```
    Ashely(P)
    Christeen(P)
    Jane(A)
    Jenny(D)
    Julia(A)
    Ketty(P)
    Maria(A)
    Meera(S)
    Priya(S)
    Samantha(D)
    There are a total of 2 doctors.
    There are a total of 2 singers.
    There are a total of 3 actors.
    There are a total of 3 professors.
  ```


**Explanation**

The results of the first query are formatted to the problem description's specifications.
The results of the second query are ascendingly ordered first by number of names corresponding to each profession (2≤2≤3≤3), and then alphabetically by profession (doctor ≤ singer, and actor ≤ professor).


**Solution**
```sql
(SELECT CONCAT(Name,'(',LEFT(Occupation,1),')') AS a
FROM Occupations)
UNION
(SELECT CONCAT('There are a total of',' ',COUNT(Occupation),' ', lower(Occupation),'s','.')
FROM Occupations
GROUP BY Occupation)
ORDER BY a
```



**[Binary Tree Nodes](https://www.hackerrank.com/challenges/binary-search-tree-1)**

You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.

|  Column | Type |
|---|---|
| N  | Integer |
| P | Integer |

Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:

    Root: If node is root node.
    Leaf: If node is leaf node.
    Inner: If node is neither root nor leaf node.

**Sample Input**

|  N | P |
|---|---|
| 1  | 2 |
| 3 | 2 |
| 6 | 8  |
| 9 | 8 |
|2 | 5 |
|8| 5 | 
|5 | Null |

**Sample Output**
```
  1 Leaf
  2 Inner
  3 Leaf
  5 Root
  6 Leaf
  8 Inner
  9 Leaf
```

**Explanation**

The Binary Tree below illustrates the sample:

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/5772428a-62d2-4cc7-bf67-d66f66c8532f)



**Solution**
```sql
SELECT N,
    (CASE
        WHEN P IS NULL THEN 'Root'
        WHEN N IN (SELECT DISTINCT(P) FROM BST WHERE P IS NOT NULL) THEN 'Inner'
        ELSE 'Leaf'
        END)
FROM BST
ORDER BY N
```

**[Occupations](https://www.hackerrank.com/challenges/occupations)**

Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.

Note: Print NULL when there are no more names corresponding to an occupation.

**Input Format**

The OCCUPATIONS table is described as follows:

|  Column | Type |
|---|---|
| Name  | Striing |
| Occupation | String |

Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

**Sample Input**

|  Name | Occupation |
|---|---|
| Samantha  | Doctor |
| Julia | Actor |
| Maria | Actor  |
| Meera | Singer |
|Ashely | Professor |
|Ketty| Professor | 
|Christeen | Professor |
|Jane| Actor)|
|Jenny| Doctor |
|Priya| Singer |


**Sample Output**
```
Jenny    Ashley     Meera  Jane
Samantha Christeen  Priya  Julia
NULL     Ketty      NULL   Maria
```

**Explanation**

The first column is an alphabetically ordered list of Doctor names.
The second column is an alphabetically ordered list of Professor names.
The third column is an alphabetically ordered list of Singer names.
The fourth column is an alphabetically ordered list of Actor names.
The empty cell data for columns with less than the maximum number of names per occupation (in this case, the Professor and Actor columns) are filled with NULL values.

**Solution**
```sql
CREATE VIEW pq AS (
    SELECT 
        CASE WHEN occupation = 'Doctor' THEN name END AS 'Doctor',
        CASE WHEN occupation = 'Professor' THEN name END AS 'Professor',
        CASE WHEN occupation = 'Singer' THEN name END AS  'Singer',
        CASE WHEN occupation = 'Actor' THEN name END AS  'Actor',
        ROW_NUMBER() OVER (PARTITION BY occupation ORDER BY name) as cr
    FROM occupations
);

SELECT MAX(Doctor),MAX(Professor),MAX(Singer),MAX(Actor) FROM pq 
GROUP BY cr
```

**[New Companies](https://https://www.hackerrank.com/challenges/the-company)**

Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy:

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/64eada74-72e1-445b-ac93-091717e2aad4)

Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.

Note:
    The tables may contain duplicate records.
    The company_code is string, so the sorting should not be numeric. For example, if the company_codes are C_1, C_2, and C_10, then the ascending company_codes will be C_1, C_10, and C_2.

**Input Format**

The following tables contain company data:

* Company: The company_code is the code of the company and founder is the founder of the company.

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/a0f68a9f-ff28-4b99-8e77-ebc0baad78de)

* Lead_Manager: The lead_manager_code is the code of the lead manager, and the company_code is the code of the working company.

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/1aadc71b-4ad8-4ef9-ae3d-ab3e48c63550)

* Senior_Manager: The senior_manager_code is the code of the senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/d8b8ab96-b871-45c8-a7bc-8ca4a7fd4030)

* Manager: The manager_code is the code of the manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/17b14e0e-63db-458f-8244-fc480f173699)

* Employee: The employee_code is the code of the employee, the manager_code is the code of its manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/4a290bf8-8d06-44fc-92c1-c154a182836b)

**Sample Input**

Company Table:

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/4f7b56ef-0ede-48d7-b4d8-35b57d085153)

Lead_Manager Table: 

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/2a1cef32-4bef-470d-8a8c-ed8847bd9d56)

Senior_Manager Table: 

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/564a5a3e-020f-46f8-91d5-bcc64959708d)

Manager Table: 

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/b27ebcc6-4988-46e6-91a8-73e817b3e5c7)

Employee Table: 

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/1ed1f426-59da-449e-ad4d-1df1444e1bec)


**Sample Output**
```
C1 Monika 1 2 1 2
C2 Samantha 1 1 2 2
```

**Explanation**

In company C1, the only lead manager is LM1. There are two senior managers, SM1 and SM2, under LM1. There is one manager, M1, under senior manager SM1. There are two employees, E1 and E2, under manager M1.
In company C2, the only lead manager is LM2. There is one senior manager, SM3, under LM2. There are two managers, M2 and M3, under senior manager SM3. There is one employee, E3, under manager M2, and another employee, E4, under manager, M3.

**Solution**
```sql
SELECT c.company_code, c.founder,
COUNT(DISTINCT lm.lead_manager_code),
COUNT(DISTINCT sm.senior_manager_code),
COUNT(DISTINCT m.manager_code),
COUNT(DISTINCT e.employee_code)
FROM Company c
JOIN Lead_Manager lm
USING (company_code)
JOIN Senior_Manager sm
USING (company_code)
JOIN Manager m
USING (company_code)
JOIN Employee e
USING (company_code)
GROUP BY c.company_code, c.founder
ORDER BY c.company_code;
```


**[Top Competitors](https://www.hackerrank.com/challenges/full-score)**

Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.


**Input Format**

The following tables contain contest data:

Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker. 

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/e8cacb36-1b36-4ede-9b35-64f1cd95ff13)

Difficulty: The difficult_level is the level of difficulty of the challenge, and score is the score of the challenge for the difficulty level.

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/77d5a05b-4884-44a9-aee2-504a215909d4)

Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge.

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/b9ee1109-09b9-4e95-a8d4-c8e45670a16a)

Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission.

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/082fbbe5-6a5d-41c6-beaa-ff249c677dde)

**Sample Input**

Hackers Table:

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/5c00b194-6c51-4abf-91fc-aab4c05a9b71)

Difficulty Table:

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/888eb97f-a66b-43bf-9b01-02ef20a8dab9)

Challenges Table:

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/53538435-fab7-4472-80d4-fcd0280344a4)

Submissions Table:

![afbeelding](https://github.com/MarkoButorac/SQL-HackerRank/assets/141552522/9a01dd8f-cb4f-4e95-a7c7-73496b740f43)

**Sample Output**

```
90411 Joe
```

**Explanation**

Hacker 86870 got a score of 30 for challenge 71055 with a difficulty level of 2, so 86870 earned a full score for this challenge.
Hacker 90411 got a score of 30 for challenge 71055 with a difficulty level of 2, so 90411 earned a full score for this challenge.
Hacker 90411 got a score of 100 for challenge 66730 with a difficulty level of 6, so 90411 earned a full score for this challenge.
Only hacker 90411 managed to earn a full score for more than one challenge, so we print the their hacker_id and name as
space-separated values.

**Solution**
```sql
SELECT h.hacker_id, h.name
FROM Hackers h
JOIN Submissions s USING (hacker_id)
JOIN Challenges c USING (challenge_id)
JOIN Difficulty d ON c.difficulty_level = d.difficulty_level AND s.score = d.score
GROUP BY h.hacker_id, h.name
HAVING COUNT(c.challenge_id) > 1
ORDER BY COUNT(c.challenge_id) DESC, h.hacker_id ASC;
```







