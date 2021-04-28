# Retrieving Entities

Once you have an entity and its associated database table you can start retrieving data from your database.


You can configure your query to retrieve entities using any qb method.  It is highly recommended you become familiar with the [qb documentation.](https://qb.ortusbooks.com/)


## Active Record

You start every interaction with Quick with an instance of an entity. The easiest way to do this is using WireBox. 'getInstance' is available in all handlers by default. WireBox can easily be injected in to any other class you need using 'inject="wirebox"`.

Quick is backed by qb, a CFML Query Builder. With this in mind, think of retrieving records for your entities like interacting with qb. For example:

```javascript
var users = getInstance( "User" ).all();

for ( var user in users ) {
    writeOutput( user.getUsername() );
}
```

In addition to using 'for' you can utilize the 'each' function on arrays. For example:

```javascript
var users = getInstance( "User" ).all();

prc.users.each( function( user ) {
    writeOutput( user.getUsername() );
});
```

You can add constraints to the query just the same as you would using qb directly:

```javascript
var users = getInstance( "User" )
    .where( "active", 1 )
    .orderByDesc( "username" )
    .limit( 10 )
    .get();
```


For more information on what is possible with qb, check out the [qb documentation](https://qb.ortusbooks.com).


## Quick Service

A second way to retrieve results is to use a Quick Service. It is similar to a 'VirtualEntityService' from cborm.

The easiest way to create a Quick Service is to inject it using the 'quickService:' dsl:

```javascript
component {

    property name="userService" inject="quickService:User"

}
```

If you have a existing Service, and you would like to extend the quickService, you can extend the quikc.models.BaseService and then call super.init inside of the service init function passing the name of the entity (for example your User Entity) shown below:

```javascript
component singleton extends="quick.models.BaseService" {

    function init(){
        super.init( "User" );
    }

}
```

Any method you can call on an entity can be called on the service.  A new entity will be used for all calls to a Quick Service.

```javascript
var users = userService
    .where( "active", 1 )
    .orderByDesc( "username" )
    .limit( 10 )
    .get();
```

## Aggregates

Calling qb's aggregate methods \('count`, 'max`, etc.\) will return the appropriate value instead of an entity or collection of entities.

### existsOrFail






Returns true if any entities exist with the configured query. If no entities exist, it throws an EntityNotFound exception.

```javascript
var doesUserExist = getInstance( "User" )
    .existsOrFail( rc.userID );
```

## Retrieval Methods

### all





Retrieves all the records for an entity. Calling 'all' will ignore any non-global constraints on the query.

```javascript
var users = getInstance( "User" ).all();
```

### get





Executes the configured query, eager loads any relations, and returns the entities in a new collection.

```javascript
var posts = getInstance( "Post" )
    .whereNotNull( "publishedDate" )
    .get();
```

### paginate






Executes the configured query, eager loads any relations, and returns the entities in the configured qb pagination struct.

```javascript
var posts = getInstance( "Post" )
    .whereNotNull( "publishedDate" )
    .paginate( rc.page, rc.maxrows );
```

```javascript
// default response example
{
    "results": [ User#1, User#2, ... ],
    "pagination": {
        "totalPages": 2,
        "maxRows": 25,
        "offset": 0,
        "page": 1,
        "totalRecords": 40
    }
}
```

### simplePaginate






Executes the configured query, eager loads any relations, and returns the entities in the configured qb simple pagination struct.

```javascript
var posts = getInstance( "Post" )
    .whereNotNull( "publishedDate" )
    .simplePaginate( rc.page, rc.maxrows );
```

```javascript
// default response example
{
    "results": [ User#1, User#2, ... ],
    "pagination": {
        "hasMore": true,
        "maxRows": 25,
        "offset": 0,
        "page": 1
    }
}
```

### first





Executes the configured query and returns the first entity found.  If no entity is found, returns 'null`.

```javascript
var user = getInstance( "User" )
    .where( "username", rc.username )
    .first();
```

### firstWhere








Adds a basic where clause to the query and returns the first result.

```javascript
var user = getInstance( "User" )
    .firstWhere( "username", rc.username );
```

### firstOrFail





Executes the configured query and returns the first entity found.  If no entity is found, then an 'EntityNotFound' exception is thrown with the given or default error message.

```javascript
var user = getInstance( "User" )
    .where( "username", rc.username )
    .firstOrFail();
```

### firstOrNew







Finds the first matching record or returns an unloaded new entity.

```javascript
var user = getInstance( "User" )
    .firstOrNew( { "username": rc.username } );
```

### firstOrCreate







Finds the first matching record or creates a new entity.

```javascript
var user = getInstance( "User" )
    .firstOrCreate( { "username": rc.username } );
```

### find





Returns the entity with the id value as the primary key. If no record is found, it returns null instead.

```javascript
var user = getInstance( "User" )
    .find( rc.userID );
```

### findOrFail






Returns the entity with the id value as the primary key. If no record is found, it throws an 'EntityNotFound' exception.

```javascript
var user = getInstance( "User" )
    .findOrFail( rc.userID );
```

### findOrNew







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

### findOrCreate







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

## Hydration Methods

Hydration is a term to describe filling an entity with a struct of data and then marking it as loaded, without doing any database queries.  For example, this might be useful when hydrating a user from session data instead of doing a query every request.

### hydrate






Hyrdates an entity from a struct of data.  Hydrating an entity fills the entity and then marks it as loaded.

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

## Custom Collections

If you would like collections of entities to be returned as something besides an array, you can override the 'newCollection' method.  It receives the array of entities.  You can return any custom collection you desire.

### newCollection





Returns a new collection of the given entities. It is expected to override this method in your entity if you need to specify a different collection to return. You can also call this method with no arguments to get an empty collection.

```javascript
// Post.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function newCollection( array entities = [] ) {
        return variables._wirebox.getInstance(
            name = "extras.QuickCollection",
            initArguments = {
                "collection" = arguments.entities
            }
        );
    }

}
```

