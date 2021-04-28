# Creating New Entities

## save

New Quick entities can be created and persisted to the database by creating a new entity instance, setting the attributes on the entity, and then calling the 'save' method.

```javascript
var user = getInstance( "User" );
user.setUsername( "JaneDoe" );
user.setEmail( "jane@example.com" );
user.setPassword( "mypass1234" );
user.save();
```

When we call 'save`, the record is persisted from the database and the primary key is set to the auto-generated value \(if any\).

We can shortcut the setters above using a 'fill' method.

## fill

Finds the first matching record or creates a new entity.






Sets attributes data from a struct of key / value pairs. This method does the following, in order:

1. Guard against read-only attributes.
2. Attempt to call a relationship setter.
3. Calls custom attribute setters for attributes that exist.
4. Throws an error if an attribute does not exist \(if 'ignoreNonExistentAttributes' is 'false' which is the default\).

```javascript
var user = getInstance( "User" );
user.fill( {
    "username": "JaneDoe",
    "email": "jane@example.com",
    "password": "mypass1234"
} );
user.save();
```

## populate






Populate is simply an alias for 'fill`. Use whichever one suits you best.

## create






Creates a new entity with the given attributes and then saves the entity.

```javascript
var user = getInstance( "User" ).create( {
    "username": "JaneDoe",
    "email": "jane@example.com",
    "password": "mypass1234"
} );
```

There is no need to call 'save' when using the 'create' method.

## firstOrNew







Finds the first matching record or returns an unloaded new entity.

```javascript
var user = getInstance( "User" )
    .firstOrNew( { "username": rc.username } );
```

## firstOrCreate







Finds the first matching record or creates a new entity.

```javascript
var user = getInstance( "User" )
    .firstOrCreate( { "username": rc.username } );
```

## findOrNew







Returns the entity with the id value as the primary key. If no record is found, it returns a new unloaded entity.

```javascript
var user = getInstance( "User" ).findOrNew(
    9999,
      {
              "firstName" : "doesnt",
              "lastName"  : "exist"
      }
);
```

## findOrCreate







Returns the entity with the id value as the primary key. If no record is found, it returns a newly created entity.

```javascript
var user = getInstance( "User" ).findOrCreate(
    9999,
      {
        "username"  : "doesntexist",
              "firstName" : "doesnt",
              "lastName"  : "exist",
              "password"  : "secret"
      }
);
```

## updateOrCreate







Updates an existing record or creates a new record with the given attributes.

```javascript
var user = getInstance( "User" ).updateOrCreate( {
    "username": "newuser"
} );
```

## Hydration Methods

Hydration is a term to describe filling an entity with a struct of data and then marking it as loaded, without doing any database queries. For example, this might be useful when hydrating a user from session data instead of doing a query every request.

### hydrate






Hyrdates an entity from a struct of data. Hydrating an entity fills the entity and then marks it as loaded.

If the entity's keys are not included in the struct of data, a 'MissingHydrationKey' is thrown.

```javascript
var user = getInstance( "User" ).hydrate( {
    "id": 4,
    "username": "JaneDoe",
    "email": "jane@example.com",
    "password": "mypass1234"
} );

user.isLoaded(); // true
```

### hydrateAll






Hydrates a new collection of entities from an array of structs.

```javascript
var users = getInstance( "User" ).hydrateAll( [
    {
        "id": 3,
        "username": "JohnDoe",
        "email": "john@example.com",
        "password": "mypass4321"
    },
    {
        "id": 4,
        "username": "JaneDoe",
        "email": "jane@example.com",
        "password": "mypass1234"
    }
] );
```

