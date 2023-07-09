# A Hands-On Guide to MySQL

#### In:
```
SELECT * FROM users WHERE dept IN ('design', 'sales');
```

#### Select:
```
SELECT * FROM users;
SELECT first_name, last_name FROM users;
```
#### Join:

##### Math:

#### Indexing:

#### Selecting titles with % and _ in them:

##### Data Types:
```
# The common ones are

# INTEGERS
TINYINT # 127 to -128
SMALLINT # 32768 to -32767
MEDIUMINT # 8388608 to -8388608
INT # 2^31 to -2^31 -1
BIGINT # 2^63 to -2^63 - 1
FLOAT
DOUBLE

# STRINGS
CHAR # Fixed length string
VARCHAR # Variable length string
BLOB # 2^16 bytes
ENUM # Limited number of total values
SET # List of possible legal character strings, can contain more than just one entry unlike ENUM

# DATE and TIME
DATE # YYYY-MM-DD
TIME # HH:MM:SS
DATETIME # YYYY-MM-DD HH:MM:SS
TIMESTAMP # YYYYMMDDHHMMSS
YEAR # YYYY
```


#### Aggregate functions
