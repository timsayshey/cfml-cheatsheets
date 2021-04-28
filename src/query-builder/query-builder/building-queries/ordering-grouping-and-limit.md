# Order By

The orderBy method seems simple but has a lot of depth depending on the type of arguments you pass in.


Calling orderBy multiple times appends to the order list.


## Order By \(String\)







```javascript
query.from( "users" )
    .orderBy( "email" );
```






Calling orderBy multiple times will append to the order list.


```javascript
query.from( "users" )
    .orderBy( "email" )
    .orderBy( "username", "desc" );
```






You can also provide an [Expression](https://qb.ortusbooks.com/query-builder/building-queries/raw-expressions.md).


```javascript
query.from( "users" )
    .orderBy( query.raw( "DATE(created_at)" ) );
```






## Order By \(List\)







```javascript
query.from( "users" )
    .orderBy( "email|asc,username", "desc" );
```






## Order By \(Array of Strings\)







```javascript
query.from( "users" )
    .orderBy( [ "email|asc", "username" ], "desc" );
```






## Order By \(Array of Structs\)







```javascript
query.from( "users" )
    .orderBy( [
        { "column": "email", "direction": "asc" },
        "username"
    ], "desc" );
```






## Order By \(Subquery\)






You can order with a subquery using either a function or a QueryBuilder instance.


```javascript
query.from( "users" )
    .orderBy( function( q ) {
        q.selectRaw( "MAX(created_date)" )
            .from( "logins" )
            .whereColumn( "users.id", "logins.user_id" );
    } );
```








## Order By Raw







```javascript
query.from( "users" )
    .orderByRaw( "CASE WHEN status = ? THEN 1 ELSE 0 END DESC", [ 1 ] );
```






## clearOrders





Clears the currently configured orders for the query.  Usually used by downstream libraries like [Quick](https://qb.ortusbooks.com/query-builder/building-queries/https://quick.ortusbooks.com/).


```javascript
query.from( "users" )
    .orderBy( "email" )
    .clearOrders();
```






## reorder






Clears configured orders for query and sets the new orders passed in.  Any valid argument to [orderBy](https://qb.ortusbooks.com/query-builder/building-queries/ordering-grouping-and-limit.md) can be passed here.  Usually used by downstream libraries like [Quick](https://qb.ortusbooks.com/query-builder/building-queries/https://quick.ortusbooks.com/).


```javascript
query.from( "users" )
    .orderBy( "email" )
    .reorder( "username" );
```






