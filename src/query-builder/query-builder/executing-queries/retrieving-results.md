# Retrieving Results

## get






The get method is the most common method used for retrieving results.


```javascript
query.from( "users" ).get();
```






`get can also take a list or array of columns to use as a shortcut.


```javascript
query.from( "users" ).get( [ "id", "name" ] );
```






## first





If you just need to retrieve a single row from the database table, you may use the first method.


```javascript
query.from( "users" ).first();
```






## values






If you don't even need an entire row, you may extract a single value from each record using the values method.


```javascript
query.from( "users" ).values( "firstName" );
```



```text
[ "jon", "jane", "jill", ...
]
```


## value








This method is similar to values except it only returns a single, simple value.


```javascript
query.from( "users" ).value( "firstName" );
```



```text
"jon"
```


If no records are returned from the query, one of two things will happen.

## chunk







Large datasets can be broken up and retrieved in chunks.


```javascript
query.from( "users" ).chunk( 100, function( users ) {
    // Process the users here
    // Returning false from the callback stops processing
} );
```


## paginate







Generates a pagination struct along with the results of the executed query.


```javascript
query.from( "users" )
    .paginate();
```



```javascript
{
    "pagination": {
        "maxRows": 25,
        "offset": 0,
        "page": 1,
        "totalPages": 2,
        "totalRecords": 45
    },
    "results": [ { /* ... */ }, ]
}
```


## simplePaginate







Generates a simple pagination struct along with the results of the executed query.


```javascript
query.from( "users" )
    .simplePaginate();
```



```javascript
{
    "pagination": {
        "maxRows": 25,
        "offset": 0,
        "page": 1,
        "hasMore": true
    },
    "results": [ { /* ... */ }, ]
}
```


### Custom Pagination Collectors

A pagination collector is the name given to the struct returned from calling the [paginate](retrieving-results.md#paginate) method.

#### generateWithResults



You can set your custom pagination collector either in the constructor using the paginationCollector argument or by calling setPaginationCollector on a query builder instance.



