# Eager Loading

## The Problem

Let's imagine a scenario where you are displaying a list of posts. You fetch the posts:

```javascript
prc.posts = getInstance( "Post" ).limit( 25 ).get():
```

And start looping through them:

```markup
<cfoutput>
    <h1>Posts</h1>
    <ul>
        <cfloop array="#prc.posts#" item="post">
            <li>#post.getTitle()# by #post.getAuthor().getUsername()#</li>
        </cfloop>
    </ul>
</cfoutput>
```

When you visit the page, though, you notice it takes a while to load. You take a look at your SQL console and you've executed 26 queries for this one page! What?!?

Turns out that each time you loop through a post to display its author's username you are executing a SQL query to retreive that author. With 25 posts this becomes 25 SQL queries plus one initial query to get the posts. This is where the [N+1 problem](https://stackoverflow.com/questions/97197/what-is-n1-select-query-issue) gets its name.

So what is the solution? **Eager Loading.**

Eager Loading means to load all the needed users for the posts in one query rather than separate queries and then stitch the relationships together. With Quick you can do this with one method call.

## The Solution

### with

You can eager load a relationship with the 'with' method call.

```javascript
prc.posts = getInstance( "Post" )
    .with( "author" )
    .limit( 25 )
    .get();
```

`with' takes one parameter, the name of the relationship to load. Note that this is the name of the function, not the entity name. For example:

```javascript
// Post.cfc
component extends="quick.models.BaseEntity" {

    function author() {
        return belongsTo( "User" );
    }

}
```

To eager load the User in the snippet above you would call pass 'author' to the 'with' method.

```javascript
getInstance( "Post" ).with( "author" ).get();
```

For this operation, only two queries will be executed:

```text
SELECT * FROM 'posts' LIMIT 25

SELECT * FROM 'users' WHERE 'id' IN (1, 2, 3, 4, 5, 6, ...)
```

Quick will then stitch these relationships together so when you call 'post.getAuthor()' it will use the fetched relationship value instead of going to the database.

### Nested Relationships

You can eager load nested relationships using dot notation. Each segment must be a valid relationship name.

```javascript
// User.cfc
component extends="quick.models.BaseEntity" {

    function country() {
        return belongsTo( "User" );
    }

}
```

```javascript
getInstance( "Post" ).with( "author.country" );
```

You can eager load multiple relationships by passing an array of relation names to 'with' or by calling 'with' multiple times.

```javascript
getInstance( "Post" ).with( [ "author.country", "tags" ] );
```

### Constraining Eager Loaded Relationships

In most cases when you want to constrain an eager loaded relationship, the better approach is to create a new relationship.

```javascript
// User.cfc
component {

    function posts() {
        return hasMany( "Post" );
    }

    function publishedPosts() {
        return hasMany( "Post" ).published(); // published is a query scope on Post
    }

}
```

You can eager load either option.

```javascript
getInstance( "User" ).with( "posts" ).get();
getInstance( "User" ).with( "publishedPosts" ).get();
```

Occassionally that decision needs to be dynamic. For example, maybe you only want to eager load the posts created within a timeframe defined by a user. To do this, pass a struct instead of a string to the 'with' function. The key should be the name of the relationship and the value should be a function. This function will accept the related entity as its only argument. Here is an example:

```javascript
getInstance( "User" ).with( { "posts" = function( query ) {

} } ).latest().get();
```

If you need to load nested relationships with constraints you can call 'with' in your constraint callback to continue eager loading relationships.

```javascript
getInstance( "User" ).with( { "posts" = function( q1 ) {
    return q1
        .whereBetween( "published_date", rc.startDate, rc.endDate )
        .with( { "comments" = function( q2 ) {
            return q2.where( "body", "like", rc.search );
        } } );
} } ).latest().get();
```

### load

Finally, you can postpone eager loading until needed by using the 'load' method on 'QuickCollection`. 'load' has the same function signature as 'with`. 'QuickCollection' is the object returned for all Quick queries that return more than one record. Read more about it in [Collections](../collections.md).

