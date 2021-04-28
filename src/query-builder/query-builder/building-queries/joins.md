# Joins
Join clauses range from simple to complex including joining complete subqueries on multiple conditions. qb has your back with all of these use cases.

## join

Applies a join to the query. The simplest join is to a table based on two columns:

```javascript
query.from( "users" )
    .join( "posts", "users.id", "=", "posts.author_id" );
```

When doing a simple join using = as the operator, you can omit it and pass just the column names:

```javascript
query.from( "users" )
    .join( "posts", "users.id", "posts.author_id" );
```

## joinWhere

Adds a join to another table based on a WHERE clause instead of an ON clause.

```javascript
query.from( "users" )
    .joinWhere( "contacts", "contacts.balance", "<", 100 );
```

For complex joins, a function can be passed to first.
## joinRaw


Uses the raw SQL provided to as the table for the join clause.

```javascript
query.from( "users" )
    .joinRaw( "posts (nolock)", "users.id", "posts.author_id" );
```
Using joinRaw will most likely tie your code to a specific database

## joinSub

Adds a join to a derived table. All the functionality of the join method applies to constrain the query.

```javascript
var sub = query.newQuery()
    .select( "id" )
    .from( "contacts" )
    .whereNotIn( "id", [ 1, 2, 3 ] );
    query.from( "users as u" )
    .joinSub( "c", sub, "u.id", "=", "c.id" );
```

## leftJoin

```javascript
query.from( "posts" )
    .leftJoin( "users", "users.id", "posts.author_id" );
```

## leftJoinRaw

Uses the raw SQL provided to as the table for the left join clause. All the other functionality of leftJoinRaw matches the join method.

```javascript
query.from( "posts" )
    .leftJoinRaw( "users (nolock)", "users.id", "posts.author_id" );
```

## leftJoinSub

Adds a left join to a derived table.

```javascript
var sub = query.newQuery()
    .select( "id" )
    .from( "contacts" )
    .whereNotIn( "id", [ 1, 2, 3 ] );
    query.from( "users as u" )
    .leftJoinSub( "c", sub, "u.id", "=", "c.id" );
```

## rightJoin

```javascript
query.from( "users" )
    .rightJoin( "posts", "users.id", "posts.author_id" );
```

## rightJoinRaw

Uses the raw SQL provided to as the table for the right join clause.

```javascript
query.from( "users" )
    .rightJoinRaw( "posts (nolock)", "users.id", "posts.author_id" );
```
Using rightJoinRaw will most likely tie your code to a specific database.

## rightJoinSub


Adds a right join to a derived table.

```javascript
var sub = query.newQuery()
    .select( "id" )
    .from( "contacts" )
    .whereNotIn( "id", [ 1, 2, 3 ] );
    query.from( "users as u" )
    .rightJoinSub( "c", sub, "u.id", "=", "c.id" );
```

## crossJoin

```javascript
query.from( "users" ).crossJoin( "posts" );
```

## crossJoinRaw

Uses the raw SQL provided to as the table for the cross join clause. Cross joins cannot be further constrained with on or where clauses.

```javascript
query.from( "users" ).crossJoinRaw( "posts (nolock)" );
```

## crossJoinSub

Adds a cross join to a derived table. The derived table can be defined using a QueryBuilder instance or a function just as with [joinSub](https://qb.ortusbooks.com/query-builder/building-queries/joins#joinsub).

```javascript
var sub = query.newQuery()
    .select( "id" )
    .from( "contacts" )
    .whereNotIn( "id", [ 1, 2, 3 ] );
    query.from( "users as u" ).crossJoinSub( "c", sub );
```

## newJoin

```javascript
var j = query.newJoin( "contacts" )
    .on( "users.id", "posts.author_id" );
    query.from( "users" ).join( j );
```

```javascript
// This is still an inner join because
// the JoinClause is an inner join
var j = query.newJoin( "contacts", "inner" )
    .on( "users.id", "posts.author_id" );
    query.from( "users" ).leftJoin( j );
```

## JoinClause
A JoinClause is a specialized version of a QueryBuilder. You may call on or orOn to constrain the JoinClause. You may also call any [where](https://qb.ortusbooks.com/query-builder/building-queries/wheres.md) methods.

### on

Applies a join condition to the JoinClause. An alias for whereColumn.

```javascript
var j = query.newJoin( "contacts" )
    .on( "users.id", "posts.author_id" );
    query.from( "users" ).join( j );
```

### orOn

Applies a join condition to the JoinClause using an or combinator. An alias for orWhereColumn.

```javascript
var j = query.newJoin( "contacts" )
    .on( "users.id", "posts.author_id" )
    .orOn( "users.id", "posts.reviewer_id" );
    query.from( "users" ).join( j );
```

## Preventing Duplicate Joins

You can optionally configure qb to ignore duplicate joins.

```javascript
moduleSettings = {
    "qb": {
         "preventDuplicateJoins": true
    }
};
```
