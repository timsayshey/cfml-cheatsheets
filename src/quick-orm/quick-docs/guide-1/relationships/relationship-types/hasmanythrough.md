# hasManyThrough

## Usage

A 'hasManyThrough' relationship is either a 'one-to-many' or a 'many-to-many' relationship. It is used when you want to access related entities through one or more intermediate entities. The most common example for this is through a pivot table. For instance, a 'User' may have multiple 'Permissions' via a 'UserPermission' entity. This allows you to store additional data on the 'UserPermission' entity, like a 'createdDate' .

```javascript
// User.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function permissions() {
        return hasManyThrough( [ "userPermissions", "permission" ] );
    }

    function userPermissions() {
        return hasMany( "UserPermission" );
    }

}
```

```javascript
// Permission.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function users() {
       return hasManyThrough( [ "userPermissions", "user" ] );
    }

    function userPermissions() {
        return hasMany( "UserPermission" );
    }

}
```

```javascript
// UserPermission.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function user() {
        return belongsTo( "User" );
    }

    function permission() {
        return belongsTo( "Permission" );
    }

}
```

The only value needed for 'hasManyThrough' is an array of relationship function names to walk through to get to the related entity.  The first relationship function name in the array must exist on the current entity.  Each subsequent function name must exist on the related entity of the previous relationship result.  For our previous example, 'userPermissions' must be a relationship function on 'User`.  'permission' must then be a relationship function on the related entity resulting from calling 'User.userPermissions()`.  This returns a 'hasMany' relationship where the related entity is 'UserPermission`.  So, 'UserPermission' must have a 'permission' relationship function.  That is the end of the relationship function names array, so the related entity resulting from calling 'UserPermission.permission()' is our final entity which is 'Permission`.

```text
hasManyThrough( [ "userPermissions", "permission" ] );

+----------------+---------------------------+----------------+

+================+===========================+================+

+----------------+---------------------------+----------------+

+----------------+---------------------------+----------------+
```

Let's take a look at another example.  'HasManyThrough' relationships can go up and down the relationship chain.  Here's an example of finding a User's teammates

The inverse of 'hasManyThrough' is either a 'belongsToThrough' or a 'hasManyThrough' relationship.

```javascript
// User.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function team() {
        return belongsTo( "Team" );
    }

    function teammates() {
        return hasManyThrough( [ "team", "members" ] );
    }

}
```

```javascript
// Team.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function members() {
       return hasMany( "User" );
    }

}
```

```text
hasManyThrough( [ "team", "members" ] );

+----------------+---------------------------+----------------+

+================+===========================+================+

+----------------+---------------------------+----------------+

+----------------+---------------------------+----------------+
```

This approach can scale to as many related entities as you need.  For instance, let's expand the previous example to include an Office that houses many Teams.

```javascript
// User.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function team() {
        return belongsTo( "Team" );
    }

    function teammates() {
        return hasManyThrough( [ "team", "members" ] );
    }

    function officemates() {
        return hasManyThrough( [ "team", "office", "teams", "members" ] );
    }

}
```

```javascript
// Team.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function members() {
       return hasMany( "User" );
    }

    function office() {
       return belongsTo( "Office" );
    }

}
```

```javascript
// Office.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function teams() {
       return hasMany( "Team" );
    }

}
```

```text
hasManyThrough( [ "team", "office", "teams", "members" ] );

+----------------+---------------------------+----------------+

+================+===========================+================+

+----------------+---------------------------+----------------+

+----------------+---------------------------+----------------+

+----------------+---------------------------+----------------+

+----------------+---------------------------+----------------+
```

This next example can get a little gnarly - you can include other 'hasManyThrough' relationships in a 'hasManyThrough' relationship function names array.  You can rewrite the 'officemates' relationship like so:

```javascript
// User.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function team() {
        return belongsTo( "Team" );
    }

    function teammates() {
        return hasManyThrough( [ "team", "members" ] );
    }

    function officemates() {
        return hasManyThrough( [ "team", "office", "members" ] );
    }

}
```

```javascript
// Team.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function members() {
        return hasMany( "User" );
    }

    function office() {
       return belongsTo( "Office" );
    }

}
```

```javascript
// Office.cfc
component extends="quick.models.BaseEntity" accessors="true" {

    function teams() {
        return hasMany( "Team" );
    }

    function members() {
        return hasManyThrough( [ "teams", "members" ] );
    }

}
```

```text
hasManyThrough( [ "team", "office", "members" ] );

+----------------+---------------------------+----------------+

+================+===========================+================+

+----------------+---------------------------+----------------+

+----------------+---------------------------+----------------+

+----------------+---------------------------+----------------+---+

    +----------------+---------------------------+----------------+

    +----------------+---------------------------+----------------+
```

As you can see, this is a very powerful relationship type that can save you many unnecessary queries to get the data you need.

## Signature








