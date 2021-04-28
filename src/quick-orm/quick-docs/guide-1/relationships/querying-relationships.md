# Querying Relationships

When querying an entity, you may want to restrict the query based on the existence or absence of a related entity.  You can do that using the following four methods:

## has








Checks for the existence of a relationship when executing the query.

By default, a 'has' constraint will only return entities that have one or more of the related entity.

```javascript
getInstance( "User" ).has( "posts" ).get();
```

An optional operator and count can be added to the call.

```javascript
getInstance( "User" ).has( "posts", ">", 2 ).get();
```

Nested relationships can be checked by passing a dot-delimited string of relationships.

```javascript
getInstance( "User" ).has( "posts.comments" ).get();
```

## doesntHave







Checks for the absence of a relationship when executing the query.

By default, a 'doesntHave' constraint will only return entities that have zero of the related entity.

```javascript
getInstance( "User" ).doesntHave( "posts" ).get();
```

An optional operator and count can be added to the call.

```javascript
getInstance( "User" ).doesntHave( "posts", "<=", 1 ).get();
```

Nested relationships can be checked by passing a dot-delimited string of relationships.

```javascript
getInstance( "User" ).doesntHave( "posts.comments" ).get();
```

## whereHas









When you need to have more control over the relationship constraint, you can use 'whereHas`.  This method operates similarly to 'has' but also accepts a callback to configure the relationship constraint.

The 'whereHas' callback is passed a builder instance configured according to the relationship.  You may call any entity or query builder methods on it as usual.

```javascript
getInstance( "User" )
    .whereHas( "posts", function( q ) {
	      q.where( "body", "like", "%different%" );
    } )
		.get();
```

When you specify a nested relationship, the builder instance is configured for the last relationship specified.

```javascript
getInstance( "User" )
    .whereHas( "posts.comments", function( q ) {
	      q.where( "body", "like", "%great%" );
	  } )
	  .get();
```

An optional operator and count can be added to the call, as well.

```javascript
getInstance( "User" )
    .whereHas( "posts.comments", function( q ) {
	      q.where( "body", "like", "%great%" );
	  }, ">", 2 )
	  .get();
```

## whereDoesntHave








The 'whereDoesntHave' callback is passed a builder instance configured according to the relationship.  You may call any entity or query builder methods on it as usual.

```javascript
getInstance( "User" )
    .whereDoesntHave( "posts", function( q ) {
	      q.where( "body", "like", "%different%" );
    } )
		.get();
```

When you specify a nested relationship, the builder instance is configured for the last relationship specified.

```javascript
getInstance( "User" )
    .whereDoesntHave( "posts.comments", function( q ) {
	      q.where( "body", "like", "%great%" );
	  } )
	  .get();
```

An optional operator and count can be added to the call, as well.

```javascript
getInstance( "User" )
    .whereDoesntHave( "posts.comments", function( q ) {
	      q.where( "body", "like", "%great%" );
	  }, ">", 2 )
	  .get();
```

