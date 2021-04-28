# Updating Existing Entities

## save

Updates are handled identically to inserts when using the 'save' method. The only difference is that instead of starting with a new entity, we start with an existing entity.

```javascript
var user = getInstance( "User" ).find( 1 );
user.setPassword( "newpassword" );
user.save();
```

## update

You can update multiple fields at once using the 'update' method. This is similar to the 'create' method for creating new entities.






```javascript
var user = getInstance( "User" ).find( 1 );
user.update( {
   email = "janedoe2@example.com",
   password = "newpassword"
} );
```

There is no need to call 'save' when using the 'update' method.

By default, if you have a key in the struct that doesn't match a property in the entity the 'update' method will fail. If you add the optional argument 'ignoreNonExistentAttributes' set to 'true`, those missing keys are ignored. Now you can pass the 'rc' scope from your submitted form directly into the 'update' method and not worry about any other keys in the 'rc' like 'event' that would cause the method to fail.

```javascript
var user = getInstance( "User" ).find( 1 );
user.update( rc, true );
```

## updateOrCreate







Updates an existing record or creates a new record with the given attributes.

```javascript
var user = getInstance( "User" ).updateOrCreate( {
    "username": "newuser"
} );
```

## updateAll






Updates matching entities with the given attributes according to the configured query. This is analagous to [qb's update method.](https://qb.ortusbooks.com/query-builder/executing-queries/inserts-updates-deletes#update)

```javascript
getInstance( "User" )
    .where( "lastLoggedIn", ">", dateAdd( "m", 3, now() ) )
    .updateAll( {
        "active" = 0
    } );
```

## fresh





Retrieves a new entity from the database with the same key value as the current entity. Useful for seeing any changes made to the record in the database. This function executes a query.

```javascript
var user = getInstance( "User" ).findOrFail( rc.userID );
var sameUser = user.fresh();
```

## refresh





Refreshes the attributes data for the entity with data from the database. This differs from 'fresh' in that it operates on the current entity instead of returning a new one. This function executes a query.

```javascript
var user = getInstance( "User" ).findOrFail( rc.userID );
user.refresh(); // user now has updated data from the database
```

