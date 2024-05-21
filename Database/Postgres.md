# Postgres

In Relational Database
```sql
     SELECT InitCap(C.Surname) || ', ' || InitCap(C.FirstName), A.city
       FROM Customers C JOIN Addresses A ON A.Cust_Id=C.Id -- the join
      WHERE A.city="New York"
```
In Object Relational Database
```
The same query in an object–relational database appears more simply:

    SELECT Formal( C.Name )
      FROM Customers C
     WHERE C.address.city="New York" -- the linkage is 'understood' by the ORDB
```
