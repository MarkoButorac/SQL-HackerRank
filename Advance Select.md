                                                        Advance Select
                                                    

**[The PADS](https://www.hackerrank.com/challenges/the-pads)**

Generate the following two result sets:

1. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).

2. Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format: 

        There are a total of [occupation_count] [occupation]s.

where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

Note: There will be at least two entries in the table for each type of occupation.

Input Format

|  Column | Type |
|---|---|
| Name  | String |
| Occupation  | String |

The OCCUPATIONS table is described as follows: Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

Sample Input

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

  Sample Output
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


Explanation

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

Sample Input

|  N | P |
|---|---|
| 1  | 2 |
| 3 | 2 |
| 6 | 8  |
| 9 | 8 |
|2 | 5 |
|8| 5 | 
|5 | Null |

Sample Output
```
  1 Leaf
  2 Inner
  3 Leaf
  5 Root
  6 Leaf
  8 Inner
  9 Leaf
```

Explanation

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


