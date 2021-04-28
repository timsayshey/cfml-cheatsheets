# Limit, Offset, and Pagination

## limit





Sets the limit value for the query.


```javascript
query.from( "users" )
    .limit( 5 );
```






## take





Sets the limit value for the query.  Alias for [limit](https://qb.ortusbooks.com/query-builder/building-queries/limit-offset-and-pagination#limit).


```javascript
query.from( "users" )
    .take( 5 );
```






## offset





Sets the offset value for the query.


```javascript
query.from( "users" )
    .offset( 25 );
```






## forPage






Helper method to calculate the limit and offset given a page number and count per page.


```javascript
query.from( "users" )
    .forPage( 3, 15 );
```






## simplePaginate & paginate

This method combines forPage, count, and get to create a pagination struct alongside the results. Info on the simplePaginate or paginate methods, including custom pagination collectors, can be found in the [Retreiving Results](https://qb.ortusbooks.com/query-builder/executing-queries/retrieving-results#paginate) section of the documentation.



