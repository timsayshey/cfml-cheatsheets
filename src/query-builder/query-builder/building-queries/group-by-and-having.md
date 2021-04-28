# Group By and Having

## groupBy

Passing a single string will group by that one column.
```javascript
query.from( "users" )
    .groupBy( "country" );
```

```javascript
query.from( "users" )
    .groupBy( "country,city" );
```

```javascript
query.from( "users" )
    .groupBy( [ "country", "city" ] );
```

```javascript
# Calling groupBy multiple times will to the current groups.
query.from( "users" )
    .groupBy( "country" )
    .groupBy( "city" );
```

```javascript
query.from( "users" )
    .groupBy( query.raw( "DATE(created_at)" ) );
```

## having


Adds a having clause to a query.
```javascript
query.from( "users" )
    .groupBy( "email" )
    .having( "email", ">", 1 );
```


`Expressions can be used in place of the column or the value.

```javascript
query.from( "users" )
    .groupBy( "email" )
    .having( query.raw( "COUNT(email)" ), ">", 1 );
```


