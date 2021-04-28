# Common Table Expressions \(i.e. CTEs\)

Common Table Expressions \(CTEs\) allow you to create re-usable temporal result sets.

## with

You can build a CTE using a function:
```javascript
// qb
query.with( "UserCTE", function ( q ) {
        q
            .select( [ "fName as firstName", "lName as lastName" ] )
            .from( "users" )
            .where( "disabled", 0 );
    } )
    .from( "UserCTE" )
    .get();
```

## withRecursive

```javascript
query
.withRecursive( "Hierarchy", function ( q ) {
    q.select( [ "Id", "ParentId", "Name", q.raw( "0 AS [Generation]" ) ] )
        .from( "Sample" )
        .whereNull( "ParentId" )
        // use recursion to join the child rows to their parents
        .unionAll( function ( q ) {
            q.select( [
                    "child.Id",
                    "child.ParentId",
                    "child.Name",
                    q.raw( "[parent].[Generation] + 1" )
                ] )
                .from( "Sample as child" )
                .join( "Hierarchy as parent", "child.ParentId", "parent.Id" );
        } );
    }, [ "Id", "ParentId", "Name", "Generation" ] )
    .from( "Hierarchy" )
    .get();
```


