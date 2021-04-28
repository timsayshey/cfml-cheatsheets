# Ordering By Relationships

To order by a relationship field, you will use a dot-delimited syntax.

```javascript
getInstance( "Post" ).orderBy( "author.name" );
```

The last item in the dot-delimited string should be an attribute on the related entity.

Nested relationships are also supported.  Continue to chain relationships in your dot-delimited string until arriving at the desired entity.  Remember to end with the attribute to order by.

```javascript
getInstance( "Post" ).orderBy( "author.team.name" );
```

If you desire to be explicit, you can use the 'orderByRelated' method, which is what is being called under the hood.







```javascript
getInstance( "Post" ).orderByRelated( "author.team", "name" );
// or
getInstance( "Post" ).orderByRelated( [ "author", "team" ], "name" );
```

You might prefer the explicitness of this method, but it cannot handle normal orders like 'orderBy`.  Use whichever method you prefer.

