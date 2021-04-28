# Unions

The query builder also lets you create union statements on your queries using either UNION or UNION ALL strategies.


## union

Adds a UNION statement to the query.

```javascript
query.from( "users" )
    .select( "name" )
    .where( "id", 1 )
    .union( function ( q ) {
        q.from( "users" )
            .select( "name" )
            .where( "id", 2 );
    } );
```



## unionAll





Adds a UNION ALL statement to the query.


```javascript
query.from( "users" )
    .select( "name" )
    .where( "id", 1 )
    .unionAll( function( q ) {
        q.from( "users" )
            .select( "name" )
            .where( "id", 2 );
     } );
```











