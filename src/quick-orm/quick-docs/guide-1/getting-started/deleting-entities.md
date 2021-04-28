# Deleting Entities

## delete

You can delete an entity by calling the 'delete' method on it.

```javascript
var user = getInstance( "User" ).find( 1 );
user.delete();
```


The entity will still exist in any variables you have stored it in, even though it has been deleted from the database.


## deleteAll

Just like 'updateAll`, you can delete many records from the database by specifying a query with constraints and then calling the 'deleteAll' method.





Deletes matching entities according to the configured query.

```javascript
getInstance( "User" )
    .whereActive( false )
    .deleteAll();
```

Additionally, you can pass in an array of ids to 'deleteAll' to delete only those ids.  Note that any previously configured constraints will still apply.

```javascript
getInstance( "User" ).deleteAll( [ 4, 10, 22 ] );
```

