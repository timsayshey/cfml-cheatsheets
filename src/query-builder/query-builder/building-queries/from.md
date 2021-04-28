# From

## from


Used to set the base table for the query.
```javascript
query.from( "users" );
```

## table
An alias for from where you like how calling table looks.
```javascript
query.table( "users" ).insert( { "name" = "jon" } );
```

## fromRaw

Sometimes you need more control over your from clause in order to add grammar specific instructions, such as adding SQL Server table hints to your queries.

```javascript
query.fromRaw( "[users] u (nolock)" ).get();
```

## fromSub

Complex queries often contain derived tables.

```javascript
query.select( [ "firstName", "lastName" ] )
    .fromSub( "legalUsers", function ( q ) {
        q.select( [ "lName as lastName", "fName as firstName" ] )
            .from( "users" )
            .where( "age", ">=", 21 )
        ;
    } )
    .orderBy( "lastName" )
    .get()
```
