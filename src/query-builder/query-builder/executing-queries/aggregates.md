# Aggregates

The query builder also provides a variety of aggregate methods such as count, max, min, and sum.

## exists

Returns true if the query returns any rows.  Returns false otherwise.


```javascript
query.from( "users" ).where( "username", "like", "jon%" ).exists();
```






## count






Returns an integer number of rows returned by the query.


```javascript
query.from( "users" ).count();
```












## max






Returns the maximum value for the given column.


```javascript
query.from( "users" ).max( "age" );
```






## min






Returns the minimum value for the given column.


```javascript
query.from( "users" ).min( "age" );
```






## sum






Returns the sum of all returned rows for the given column.


```javascript
query.from( "employees" ).sum( "salary" );
```






