# SQLite integration with pandas

## Creating an SQLite database from a pandas DataFrame

```python
import pandas
import sqlite3

titanic = pd.read_csv(url)

# If the database file doesn't exist it will be created. Otherwise it will be overwritten.
conn = sqlite3.connect("titanic.db")

titanic.to_sql("titanic", conn, if_exists="replace", index=False)
# index=False means we don't want to save the dataframe index as a column in the database
# this is the label that uniquely identifies each row in the dataframe
# If the table already exists, it will be replaced
```

## Executing an SQL query

```python
query = """
SELECT pclass, age, survived FROM titanic
WHERE sex='female' ORDER BY age desc
"""
# Execute the SQL query and load the results into a DataFrame
# read_sql_query is used to execute a SQL query and return the result as a DataFrame
females = pd.read_sql_query(query, conn)
```

## Cross-tabulation

```python
# Used to analyze the relationship between two attributes
print(pd.crosstab(females["Pclass"], females["Survived"]))
```

## Checking for missing values

`print("Missing age values:", titanic["Age"].isnull().sum())`

## Calculating the mean age using pandas

```python
print("Mean age (pandas):", titanic["Age"].mean(skipna=True))
# skipna=True is the default behaviour
```

## Calculating the mean age using SQL

```python

print("Mean age(SQL):", pd.read_sql("SELECT avg(Age) from titanic", conn).iloc[0, 0])
# pd.read_dql executes an SQL query and returns the result as a DataFrame
# result is 1x1 dataframe, so we use .iloc to access the scalar value
```

## Closing the connection

`conn.close()`