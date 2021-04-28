# When / Conditionals

If you store the builder object in a variable, you can use if and else statements like you would expect.


```javascript
var q = query.from( "posts" );
if ( someFlag ) {
    q.orderBy( "published_date", "desc" );
}
```


This works, but breaks chainability. To keep chainability you can use the when helper method.

## when


The when helper is used to allow conditional statements when defining queries without using if statements and having to store temporary variables.


```javascript
query.from( "posts" )
    .when( someFlag, function( q ) {
        q.orderBy( "published_date", "desc" );
    } )
    .get();
```