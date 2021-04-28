# Query Parameters and Bindings

## Custom Parameter Types

When passing a parameter to qb, it will infer the sql type to be used.  You can pass a struct with the parameters you would pass to [cfqueryparam](https://qb.ortusbooks.com/query-builder/building-queries/https://cfdocs.org/cfqueryparam).

```javascript
query.from( "users" )
    .where( "id", "=", { value = 18, cfsqltype = "CF_SQL_VARCHAR" } );
```






This can be used when inserting or updating records as well.


```javascript
query.table( "users" )
    .insert( {
        "id" = { value 1, cfsqltype = "CF_SQL_VARCHAR" },
        "age" = 18,
        "updatedDate" = { value = now(), cfsqltype = "CF_SQL_DATE" }
    } );
```






### Strict Date Detection

By default, qb will try to determine if a variable is a date using the built-in isDate function.

```javascript
moduleSettings = {
    "qb": {
        "strictDateDetection": true
    }
};
```

### Numeric SQL Type

By default, qb will use the CF_SQL_NUMERIC SQL type when it detects a numeric binding.

```javascript
moduleSettings = {
    "qb": {
        "numericSQLType": "CF_SQL_INTEGER"
    }
};
```

## Bindings

Bindings are the values that will be sent as parameters to a prepared SQL statement.

### getBindings


This method returns the current bindings in order to be used for the query.


```javascript
query.from( "users" )
    .join( "logins", function( j ) {
        j.on( "users.id", "logins.user_id" );
        j.where( "logins.created_date", ">", dateAdd( "m", -1, "01 Jun 2019" ) );
    } )
    .where( "active", 1 );
```






You can also retrieve the bindings associated to their corresponding types.

### getRawBindings





This method returns the current bindings  to be used for the query associated to their corresponding types.


```javascript
query.from( "users" )
    .join( "logins", function( j ) {
        j.on( "users.id", "logins.user_id" );
        j.where( "logins.created_date", ">", dateAdd( "m", -1, "01 Jun 2019" ) );
    } )
    .where( "active", 1 );
```






