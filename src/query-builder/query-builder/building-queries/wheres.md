# Wheres









## Where Methods

### where








Adds a where clause to a query.


```javascript
query.from( "users" )
    .where( "active", "=", 1 );
```

```javascript
query.from( "users" ).where( "last_logged_in", ">", query.raw( "NOW()" ) );
```

```javascript
query.from( "users" ).where( "active", 1 );
```

### andWhere







This method is simply an alias for [where](https://qb.ortusbooks.com/query-builder/building-queries/wheres#where) with the combinator set to "and".

### orWhere







This method is simply an alias for [where](https://qb.ortusbooks.com/query-builder/building-queries/wheres#where) with the combinator set to "or".

### whereBetween









Adds a where between clause to the query.


```javascript
query.from( "users" )
    .whereBetween( "id", 1, 2 );
```






If a function or QueryBuilder is passed it is used as a subselect expression.


```javascript
query.from( "users" )
    .whereBetween(
        "id",
        function( q ) {
            q.select( q.raw( "MIN(id)" ) )
                .from( "users" )
                .where( "email", "bar" );
        },
        builder.newQuery()
            .select( builder.raw( "MAX(id)" ) )
            .from( "users" )
            .where( "email", "bar" )
    );
```






### whereNotBetween








Adds a where not in clause to the query.  This behaves identically to the [whereBetween](https://qb.ortusbooks.com/query-builder/building-queries/wheres#wherebetween) method with the negate`flag set to true.

### whereColumn








Adds a where clause to a query that compares two columns.


```javascript
query.from( "users" )
    .whereColumn( "first_name", "=", "last_name" );
```


```javascript
query.from( "users" )
    .whereColumn( "first_name", "last_name" );
```


```javascript
query.from( "users" )
    .whereColumn( "first_name", query.raw( "LOWER(first_name)" ) );
```






### whereExists






```javascript
query.from( "orders" )
    .whereExists( function( q ) {
        q.select( q.raw( 1 ) )
            .from( "products" )
            .whereColumn( "products.id", "orders.id" );
    } );
```

### whereNotExists






Adds a where not in clause to the query.  This behaves identically to the [whereExists](https://qb.ortusbooks.com/query-builder/building-queries/wheres#whereexists) method with the negate`flag set to true.

### whereLike







A shortcut for calling [where](https://qb.ortusbooks.com/query-builder/building-queries/wheres#where) with "like" set as the operator.


```javascript
query.from( "users" )
    .whereLike( "username", "J%" );
```






### whereIn








Adds a where in clause to the query.

Pass single value, a list of values, or an array of values.

```javascript
query.from( "orders" )
    .whereIn( "id", [ 1, 4, 66 ] );
```

### whereNotIn

Adds a where not in clause to the query.

### whereRaw

Shorthand to add a raw SQL statement to the where clauses.


```javascript
query.from( "users" )
    .whereRaw(
        "id = ? OR email = ? OR is_admin = 1",
        [ 1, "foo" ]
    );
```






### whereNull







Adds a where null clause to the query.


```javascript
query.from( "users" )
    .whereNull( "id" );
```






### whereNotNull







Adds a where not in clause to the query.

## Dynamic Where Methods

qb uses onMissingMethod to provide a few different helpers when working with where... methods.

### andWhere... and orWhere...

Every where... method in qb can be called prefixed with either and or or.


```javascript
query.from( "users" )
    .where( "username", "like", "j%" )
    .andWhere( function( q ) {
        q.where( "isSubscribed", 1 )
            .orWhere( "isOnFreeTrial", 1 );
     } );
```






### where{Column}

```javascript
query.from( "users" )
    .whereUsername( "like", "j%" )
    .whereActive( 1 );
```






