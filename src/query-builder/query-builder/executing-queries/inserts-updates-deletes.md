# Inserts, Updates, and Deletes

## insert








This call must come after setting the query's table using [from](../building-queries/from.md#get) or [table](../building-queries/from.md#get-1).


You can insert a single record by passing a struct:


```javascript
query.from( "users" )
    .insert( {
        "name" = "Robert",
        "email" = "robert@test.com",
        "age" = 55
    } );
```






You can specify any [query param](../building-queries/parameters-and-bindings.md#custom-parameter-types).


```javascript
query.from( "users" )
    .insert( {
        "name" = "Robert",
        "email" = "robert@test.com",
        "age" = { value = 55, cfsqltype = "CF_SQL_INTEGER" }
    } );
```






Raw values can be supplied to an insert statement.


```javascript
query.from( "users" )
    .insert( {
        "name" = "Robert",
        "email" = "robert@test.com",
        "updatedDate" = query.raw( "NOW()" )
    } );
```






Multiple rows can be inserted in a batch by passing an array of structs to insert.



```javascript
query.from( "users" ).insert( [
    { "email" = "john@example.com", "name" = "John Doe" },
    { "email" = "jane@example.com", "name" = "Jane Doe" }
] );
```












## returning






Returning is only supported in PostgresGrammar and SqlServerGrammar.


Specifies columns to be returned from the insert query.


```javascript
query.from( "users" )
    .returning( "id" )
    .insert( {
        "email" = "foo",
        "name" = "bar"
    } );
```












## update








This call must come after setting the query's table using [from](../building-queries/from.md#get) or [table](../building-queries/from.md#get-1).


Updates a table with a struct of column and value pairs.


```javascript
query.from( "users" )
    .update( {
        "email" = "foo",
        "name" = "bar"
    } );
```






You can specify any [query param](../building-queries/parameters-and-bindings.md#custom-parameter-types)


```javascript
query.from( "users" )
    .update( {
        "email" = "foo",
        "name" = "bar",
        "updatedDate" = { value = now(), cfsqltype = "CF_SQL_TIMESTAMP" }
    } );
```






Any constraining of the update query should be done using the appropriate [WHERE](../building-queries/wheres.md) statement before calling update.


```javascript
query.from( "users" )
    .whereId( 1 )
    .update( {
        "email" = "foo",
        "name" = "bar"
    } );
```






You can update a column based on another column using a raw expression.


```javascript
query.from( "hits" )
    .where( "page", "someUrl" )
    .update( {
        "count" = query.raw( "count + 1" )
    } );
```






### Updating Null values

Null values can be inserted by using queryparam syntax:



if you are using Lucee with full null support the following \(easier\) syntax is also allowed:



## addUpdate





Adds values to a later [update](inserts-updates-deletes.md#update), similar to [addSelect](../building-queries/selects.md#get-2).


```javascript
query.from( "users" )
    .whereId( 1 )
    .addUpdate( {
        "email" = "foo",
        "name" = "bar"
    } )
    .when( true, function( q ) {
        q.addUpdate( {
            "foo": "yes"
        } );
    } )
    .when( false, function( q ) {
        q.addUpdate( {
            "bar": "no"
        } );
    } )
    .update();
```






## updateOrInsert







Performs an update statement if the configured query returns true for exists.  Otherwise, performs an insert statement.


```javascript
query.from( "users" )
    .where( "email", "foo" )
    .updateOrInsert( {
        "email" = "foo",
        "name" = "baz"
    } );
```






If the configured query returns 0 records, then an insert statement is performed.


```javascript
query.from( "users" )
    .where( "email", "foo" )
    .updateOrInsert( {
        "email" = "foo",
        "name" = "baz"
    } );
```






## delete








Deletes all records that the query returns.


```javascript
query.from( "users" )
    .where( "email", "foo" )
    .delete();
```






The id argument is a convenience to delete a single record by id.


```javascript
query.from( "users" )
    .delete( 1 );
```






