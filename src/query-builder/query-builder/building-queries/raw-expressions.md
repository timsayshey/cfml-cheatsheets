# Raw Expressions

Raw expressions are the qb escape hatch.

## raw


The sql snippet passed to raw is not processed by qb at all.


```javascript
query.from( "users" ).select( query.raw( "MAX(created_date)" ) );
```
